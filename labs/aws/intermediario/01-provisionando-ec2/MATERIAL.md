# Material de Estudo — Amazon EC2

> Resumo de apoio para o [Lab 01](README.md)

---

## O que é Amazon EC2?

**Amazon EC2** (Elastic Compute Cloud) é o serviço de computação em nuvem da AWS que permite provisionar e gerenciar **servidores virtuais** (chamados de instâncias) sob demanda. Com o EC2 você pode escolher o sistema operacional, o tipo de hardware, a região e as configurações de rede — pagando apenas pelo tempo de uso.

O EC2 é um dos serviços mais utilizados da AWS e serve como base para hospedar aplicações web, APIs, bancos de dados, pipelines de dados e praticamente qualquer carga de trabalho que precise de um servidor.

---

## Conceitos-chave

- **Instância:** Um servidor virtual executando na infraestrutura da AWS. Cada instância possui vCPUs, memória, armazenamento e rede configuráveis
- **AMI (Amazon Machine Image):** Imagem pré-configurada que contém o sistema operacional e software necessário para lançar uma instância. Funciona como um "template" do servidor
- **Key Pair (Par de Chaves):** Par de chaves criptográficas (pública e privada) usado para autenticação SSH. A AWS armazena a chave pública e você mantém a chave privada localmente
- **Security Group:** Firewall virtual que controla o tráfego de entrada (inbound) e saída (outbound) de uma instância. Funciona no nível da instância
- **Instance Type (Tipo de Instância):** Define a combinação de CPU, memória, armazenamento e rede. Exemplo: `t2.micro` oferece 1 vCPU e 1 GB de RAM
- **VPC (Virtual Private Cloud):** Rede virtual isolada onde as instâncias são executadas. Toda conta AWS possui uma VPC padrão (default)
- **Elastic IP:** Endereço IP público estático que pode ser associado a uma instância. Diferente do IP público dinâmico, que muda quando a instância é parada e reiniciada
- **EBS (Elastic Block Store):** Armazenamento em bloco persistente anexado às instâncias EC2. Funciona como um disco rígido virtual

---

## AMI — Amazon Machine Image

A AMI é o ponto de partida para qualquer instância EC2. Ela define:

- **Sistema operacional** (Amazon Linux, Ubuntu, Windows Server, etc.)
- **Arquitetura** (x86_64, arm64)
- **Software pré-instalado** (servidores web, runtimes, ferramentas)
- **Configurações de armazenamento** (tipo e tamanho dos volumes EBS)

### Tipos de AMI

| Tipo | Descrição |
|---|---|
| AMIs da AWS | Mantidas pela Amazon (ex: Amazon Linux 2023). Sempre atualizadas e gratuitas |
| AMIs do Marketplace | Criadas por terceiros, podem ter custo adicional de licenciamento |
| AMIs da comunidade | Compartilhadas publicamente por outros usuários. Use com cautela |
| AMIs personalizadas | Criadas por você a partir de uma instância existente |

No lab utilizamos o **AWS Systems Manager Parameter Store** para buscar o ID da AMI mais recente do Amazon Linux 2023, garantindo que a imagem esteja sempre atualizada.

---

## Key Pairs e Segurança de Acesso SSH

O acesso SSH a instâncias Linux na AWS é feito por meio de **pares de chaves criptográficas**:

1. **Chave pública** — armazenada pela AWS e injetada na instância durante o lançamento
2. **Chave privada** — baixada por você no momento da criação (arquivo `.pem`). A AWS **não armazena** essa chave — se perdê-la, não há como recuperá-la

### Regras importantes

- O arquivo `.pem` deve ter permissão **400** (somente leitura pelo proprietário). O SSH recusa conexões se a chave tiver permissões muito abertas
- Nunca compartilhe sua chave privada ou a adicione a repositórios Git
- O usuário padrão para conexão SSH no Amazon Linux é `ec2-user`

### Comando para conectar via SSH

```bash
ssh -i lab-ec2-key.pem ec2-user@<IP_PUBLICO>
```

---

## Security Groups — Firewall Virtual

Security Groups atuam como um **firewall no nível da instância**, controlando quais conexões são permitidas:

### Regras de entrada (Inbound)

Definem **quem pode se conectar** à instância e por qual porta/protocolo.

| Campo | Descrição | Exemplo do lab |
|---|---|---|
| Protocol | Protocolo de rede | `tcp` |
| Port | Porta de destino | `22` (SSH) |
| Source (CIDR) | Origem permitida | `0.0.0.0/0` (qualquer IP) |

### Regras de saída (Outbound)

Definem **para onde a instância pode se conectar**. Por padrão, todo tráfego de saída é permitido.

### Características importantes

- Security Groups são **stateful**: se uma conexão de entrada é permitida, a resposta automaticamente também é
- Você só pode criar regras de **permissão** (allow). Não existe regra de negação (deny)
- Uma instância pode ter múltiplos Security Groups associados
- Alterações nas regras são aplicadas **imediatamente**

---

## Tipos de Instância e Free Tier

O nome do tipo de instância segue o padrão: **família + geração + tamanho** (ex: `t2.micro`).

### Famílias mais comuns

| Família | Otimizada para | Exemplo |
|---|---|---|
| **t** (General Purpose) | Cargas variáveis com burst de CPU | t2.micro, t3.micro |
| **m** (General Purpose) | Equilíbrio entre CPU, memória e rede | m5.large |
| **c** (Compute Optimized) | Cargas intensivas de CPU | c5.xlarge |
| **r** (Memory Optimized) | Cargas que exigem muita memória | r5.large |
| **g/p** (Accelerated Computing) | Machine learning, GPUs | g4dn.xlarge |

### Free Tier para EC2

O AWS Free Tier oferece **750 horas por mês** de instâncias `t2.micro` (ou `t3.micro` em regiões onde `t2.micro` não está disponível) durante os **primeiros 12 meses** da conta AWS. Isso equivale a rodar 1 instância 24/7 durante o mês inteiro sem custo.

| Recurso Free Tier | Limite |
|---|---|
| Tipo de instância | t2.micro (1 vCPU, 1 GB RAM) |
| Horas/mês | 750 horas |
| Sistema operacional | Linux ou Windows |
| Armazenamento EBS | 30 GB (General Purpose SSD) |
| Período | 12 primeiros meses da conta |

> **Atenção:** Se você lançar mais de uma instância ao mesmo tempo, as horas são somadas. Duas instâncias rodando por 500 horas cada totalizam 1.000 horas e serão cobradas pelo excedente.

---

## Ciclo de Vida da Instância EC2

Uma instância EC2 passa por diferentes estados durante seu ciclo de vida:

```
launch → pending → running → stopping → stopped → starting → running
                      ↓                                         ↓
                 shutting-down → terminated              shutting-down → terminated
```

| Estado | Descrição | Cobrado? |
|---|---|---|
| **pending** | Instância sendo preparada para execução | Não |
| **running** | Instância em execução, acessível via rede | Sim |
| **stopping** | Instância sendo parada (somente instâncias com EBS) | Não |
| **stopped** | Instância parada — sem cobrança de computação, mas o volume EBS ainda é cobrado | Não (computação) |
| **shutting-down** | Instância sendo encerrada permanentemente | Não |
| **terminated** | Instância completamente removida. Não pode ser reiniciada | Não |

### Diferença entre Stop e Terminate

- **Stop (Parar):** A instância é desligada mas os dados no volume EBS são preservados. Ao reiniciar, ela recebe um novo IP público (a menos que tenha um Elastic IP)
- **Terminate (Encerrar):** A instância é excluída permanentemente e, por padrão, o volume EBS raiz também é removido

---

## Comandos Úteis Adicionais

### Conectar via SSH à instância

```bash
ssh -i lab-ec2-key.pem ec2-user@<IP_PUBLICO>
```

### Parar uma instância (preserva dados)

```bash
aws ec2 stop-instances --instance-ids <INSTANCE_ID>
```

### Iniciar uma instância parada

```bash
aws ec2 start-instances --instance-ids <INSTANCE_ID>
```

### Reiniciar uma instância

```bash
aws ec2 reboot-instances --instance-ids <INSTANCE_ID>
```

### Listar todas as instâncias da conta

```bash
aws ec2 describe-instances \
    --query "Reservations[].Instances[].{ID:InstanceId,Nome:Tags[?Key=='Name']|[0].Value,Estado:State.Name,Tipo:InstanceType,IP:PublicIpAddress}" \
    --output table
```

### Criar uma AMI a partir de uma instância existente

```bash
aws ec2 create-image \
    --instance-id <INSTANCE_ID> \
    --name "minha-ami-customizada" \
    --no-reboot
```

---

## Resumo de configurações do lab

| Configuração | Valor usado no lab |
|---|---|
| AMI | Amazon Linux 2023 (x86_64) |
| Tipo de instância | t2.micro (Free Tier) |
| Key Pair | lab-ec2-key (RSA) |
| Security Group | lab-ec2-sg (SSH na porta 22) |
| CIDR de acesso | 0.0.0.0/0 (qualquer IP) |
| Tag Name | lab-ec2-instance |
| Quantidade | 1 instância |

---

## Boas Práticas de Segurança

- **Restrinja o CIDR no Security Group** — em vez de `0.0.0.0/0`, use seu IP específico com `--cidr SEU_IP/32`. Você pode descobrir seu IP com `curl ifconfig.me`
- **Nunca compartilhe o arquivo `.pem`** — trate a chave privada como uma senha. Não a versione em repositórios Git
- **Use tags em todos os recursos** — facilita a identificação, organização e controle de custos. No mínimo, use a tag `Name`
- **Encerre instâncias que não estiver usando** — mesmo no Free Tier, tenha o hábito de limpar recursos após os labs
- **Evite usar a conta root** — crie um usuário IAM com permissões específicas para gerenciar EC2
- **Mantenha os Security Groups com o mínimo de regras necessárias** — abra apenas as portas que realmente precisa (princípio do menor privilégio)
- **Habilite o AWS CloudTrail** — registra todas as chamadas de API, útil para auditoria e investigação de incidentes

---

## Erros Comuns e Como Resolvê-los

| Erro | Causa | Solução |
|---|---|---|
| `UnauthorizedOperation` | Usuário IAM sem permissão para EC2 | Adicione a policy `AmazonEC2FullAccess` ao usuário ou grupo |
| `InvalidAMIID.NotFound` | ID da AMI inválido ou de outra região | Use o comando SSM do passo 1 para buscar a AMI correta na sua região |
| `InvalidKeyPair.Duplicate` | Key pair com mesmo nome já existe | Exclua com `aws ec2 delete-key-pair --key-name lab-ec2-key` e recrie |
| `InvalidGroup.Duplicate` | Security group com mesmo nome já existe | Exclua com `aws ec2 delete-security-group --group-name lab-ec2-sg` e recrie |
| `Permission denied (publickey)` ao conectar SSH | Permissão do arquivo `.pem` incorreta ou usuário errado | Execute `chmod 400 lab-ec2-key.pem` e use o usuário `ec2-user` |
| `Connection timed out` ao conectar SSH | Security Group não permite acesso na porta 22 ou IP errado | Verifique a regra inbound do Security Group e confirme o IP público |
| `InsufficientInstanceCapacity` | AWS sem capacidade para o tipo de instância na AZ | Tente outra Availability Zone ou aguarde alguns minutos |
| `InstanceLimitExceeded` | Limite de instâncias por região atingido | Encerre instâncias não utilizadas ou solicite aumento de limite |

---

## Referências

- [Documentação oficial do Amazon EC2](https://docs.aws.amazon.com/ec2/)
- [Tipos de instância EC2](https://aws.amazon.com/ec2/instance-types/)
- [AWS Free Tier — EC2](https://aws.amazon.com/free/)
- [Security Groups para EC2](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)
- [Pares de chaves EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
- [AMIs do Amazon Linux](https://docs.aws.amazon.com/linux/al2023/ug/what-is-amazon-linux.html)
- [Ciclo de vida das instâncias](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html)
