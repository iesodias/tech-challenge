# Lab AWS – Provisionar uma Instância EC2 com AWS CLI

Neste lab você vai provisionar uma instância EC2 utilizando o Free Tier da AWS (t2.micro) com o AWS CLI. Você aprenderá a buscar a AMI correta, criar um par de chaves, configurar um security group com acesso SSH e lançar sua primeira máquina virtual na nuvem.

---

## Pré-requisitos

- Conta AWS ativa com Free Tier disponível
- AWS CLI instalado e configurado (`aws configure`)
- Permissões para gerenciar EC2, SSM e VPC

---

## 1. Buscar a AMI mais recente do Amazon Linux 2023

```bash
aws ssm get-parameter \
    --name /aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64 \
    --query "Parameter.Value" \
    --output text
```

> **`aws ssm get-parameter`** — consulta o AWS Systems Manager Parameter Store para obter um parâmetro público.
> **`--name /aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64`** — caminho do parâmetro que contém o ID da AMI mais recente do Amazon Linux 2023 para arquitetura x86_64.
> **`--query "Parameter.Value"`** — extrai apenas o valor do parâmetro (o ID da AMI), filtrando o restante da resposta.
> **`--output text`** — exibe o resultado como texto simples, facilitando copiar o valor.
> **Anote o ID da AMI retornado** (ex: `ami-0abcdef1234567890`) — você precisará dele no passo 5.

---

## 2. Criar um Par de Chaves (Key Pair)

```bash
aws ec2 create-key-pair \
    --key-name lab-ec2-key \
    --query "KeyMaterial" \
    --output text > lab-ec2-key.pem && chmod 400 lab-ec2-key.pem
```

> **`aws ec2 create-key-pair`** — cria um novo par de chaves RSA para acesso SSH à instância EC2.
> **`--key-name lab-ec2-key`** — define o nome do par de chaves como `lab-ec2-key`.
> **`--query "KeyMaterial"`** — extrai apenas o conteúdo da chave privada da resposta.
> **`--output text > lab-ec2-key.pem`** — salva a chave privada no arquivo `lab-ec2-key.pem` no diretório atual.
> **`chmod 400 lab-ec2-key.pem`** — restringe as permissões do arquivo para somente leitura pelo proprietário, requisito obrigatório do SSH.

---

## 3. Criar um Security Group

```bash
aws ec2 create-security-group \
    --group-name lab-ec2-sg \
    --description "Security Group para o lab EC2 - permite acesso SSH" \
    --query "GroupId" \
    --output text
```

> **`aws ec2 create-security-group`** — cria um novo security group na VPC padrão da conta.
> **`--group-name lab-ec2-sg`** — define o nome do security group como `lab-ec2-sg`.
> **`--description`** — descrição obrigatória que identifica a finalidade do security group.
> **`--query "GroupId"`** — extrai apenas o ID do security group criado (ex: `sg-0123456789abcdef0`).
> **Anote o GroupId retornado** — você precisará dele nos passos 4 e 5.

---

## 4. Adicionar regra de entrada SSH ao Security Group

```bash
aws ec2 authorize-security-group-ingress \
    --group-name lab-ec2-sg \
    --protocol tcp \
    --port 22 \
    --cidr 0.0.0.0/0
```

> **`aws ec2 authorize-security-group-ingress`** — adiciona uma regra de entrada (inbound) ao security group.
> **`--group-name lab-ec2-sg`** — especifica o security group criado no passo anterior.
> **`--protocol tcp`** — define o protocolo como TCP, necessário para conexões SSH.
> **`--port 22`** — libera a porta 22, porta padrão do SSH.
> **`--cidr 0.0.0.0/0`** — permite acesso de qualquer endereço IP. Em ambientes de produção, restrinja ao seu IP com `--cidr SEU_IP/32`.

---

## 5. Provisionar a instância EC2

```bash
aws ec2 run-instances \
    --image-id <AMI_ID> \
    --instance-type t2.micro \
    --key-name lab-ec2-key \
    --security-groups lab-ec2-sg \
    --count 1 \
    --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=lab-ec2-instance}]' \
    --query "Instances[0].InstanceId" \
    --output text
```

> **`aws ec2 run-instances`** — lança uma nova instância EC2 na AWS.
> **`--image-id <AMI_ID>`** — substitua `<AMI_ID>` pelo ID da AMI obtido no passo 1 (ex: `ami-0abcdef1234567890`).
> **`--instance-type t2.micro`** — tipo de instância elegível ao Free Tier (1 vCPU, 1 GB RAM). Gratuito por até 750 horas/mês no primeiro ano.
> **`--key-name lab-ec2-key`** — associa o par de chaves criado no passo 2 para acesso SSH.
> **`--security-groups lab-ec2-sg`** — associa o security group criado no passo 3.
> **`--count 1`** — lança exatamente 1 instância.
> **`--tag-specifications`** — adiciona a tag `Name=lab-ec2-instance` para facilitar a identificação no console.
> **Anote o InstanceId retornado** (ex: `i-0123456789abcdef0`) — você precisará dele nos próximos passos.

---

## 6. Verificar o status da instância

```bash
aws ec2 describe-instances \
    --filters "Name=tag:Name,Values=lab-ec2-instance" \
    --query "Reservations[0].Instances[0].{ID:InstanceId,Estado:State.Name,Tipo:InstanceType}" \
    --output table
```

> **`aws ec2 describe-instances`** — consulta informações detalhadas sobre instâncias EC2.
> **`--filters "Name=tag:Name,Values=lab-ec2-instance"`** — filtra a consulta pela tag `Name` com o valor definido no passo anterior.
> **`--query`** — seleciona apenas o ID da instância, o estado atual e o tipo, formatando como campos nomeados.
> **`--output table`** — exibe os resultados em formato de tabela legível.
> Aguarde até que o campo **Estado** mostre `running` antes de prosseguir. Se mostrar `pending`, execute o comando novamente após alguns segundos.

---

## 7. Obter o endereço IP público da instância

```bash
aws ec2 describe-instances \
    --filters "Name=tag:Name,Values=lab-ec2-instance" \
    --query "Reservations[0].Instances[0].PublicIpAddress" \
    --output text
```

> **`aws ec2 describe-instances`** — consulta os detalhes da instância EC2.
> **`--filters "Name=tag:Name,Values=lab-ec2-instance"`** — filtra pela tag `Name` para localizar a instância do lab.
> **`--query "Reservations[0].Instances[0].PublicIpAddress"`** — extrai apenas o endereço IP público atribuído à instância.
> Com o IP público, você pode conectar via SSH usando: `ssh -i lab-ec2-key.pem ec2-user@<IP_PUBLICO>`

---

## 8. Limpeza dos recursos

```bash
aws ec2 terminate-instances \
    --instance-ids <INSTANCE_ID> \
    --query "TerminatingInstances[0].CurrentState.Name" \
    --output text && \
aws ec2 wait instance-terminated \
    --instance-ids <INSTANCE_ID> && \
aws ec2 delete-security-group \
    --group-name lab-ec2-sg && \
aws ec2 delete-key-pair \
    --key-name lab-ec2-key && \
rm -f lab-ec2-key.pem
```

> **`aws ec2 terminate-instances`** — encerra a instância EC2 especificada. Substitua `<INSTANCE_ID>` pelo ID obtido no passo 5.
> **`aws ec2 wait instance-terminated`** — aguarda até que a instância esteja completamente terminada antes de prosseguir. Isso é necessário pois o security group só pode ser excluído após a instância ser removida.
> **`aws ec2 delete-security-group`** — exclui o security group `lab-ec2-sg` criado no passo 3.
> **`aws ec2 delete-key-pair`** — exclui o par de chaves `lab-ec2-key` armazenado na AWS.
> **`rm -f lab-ec2-key.pem`** — remove o arquivo da chave privada do disco local.
> **Importante:** execute todos os comandos em sequência para garantir que nenhum recurso permaneça ativo e gere custos.

---

## 🎉 Finalizou o lab? Compartilhe!

Use o template abaixo para postar no LinkedIn — basta copiar, ajustar o que quiser e publicar!

```
☁️ Mais um lab concluído!

Hoje aprendi a provisionar uma instância EC2 usando o AWS CLI.

✅ O que pratiquei:
• Busquei a AMI mais recente e criei Key Pair e Security Group para acesso SSH
• Provisionei uma instância EC2 t2.micro (Free Tier) e verifiquei o status e IP público
• Limpei todos os recursos criados para evitar custos — instância, security group e key pair

📖 Lab completo e gratuito:
https://github.com/iesodias/tech-challenge/blob/main/labs/aws/intermediario/01-provisionando-ec2/README.md

🗂️ Repositório com todos os labs:
https://github.com/iesodias/tech-challenge

#AWS #EC2 #Cloud #CloudComputing #TechChallenge #AprendizadoContínuo #DevOps
```

---
