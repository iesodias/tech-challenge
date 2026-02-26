# Lab AWS – Instalar e Configurar o AWS CLI

Neste lab você vai instalar o AWS CLI na sua máquina, criar suas credenciais de acesso no Console AWS e realizar os primeiros comandos para validar o funcionamento da ferramenta. O AWS CLI é a interface oficial de linha de comando da Amazon para gerenciar recursos AWS de forma rápida e automatizável.

---

## Pré-requisitos

- Conta AWS ativa (gratuita ou paga)
- Acesso ao terminal (Linux, macOS ou Windows)
- Conexão com a internet
- Para macOS: Homebrew instalado (`https://brew.sh`)

---

## 1. Instalar o AWS CLI no Linux (Ubuntu/Debian)

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && unzip awscliv2.zip && sudo ./aws/install
```

> **`curl "..."`** — faz o download do pacote oficial do AWS CLI v2 diretamente dos servidores da Amazon.
> **`-o "awscliv2.zip"`** — salva o arquivo baixado com o nome `awscliv2.zip` no diretório atual.
> **`unzip awscliv2.zip`** — descompacta o pacote baixado, criando a pasta `aws/` com os arquivos de instalação.
> **`sudo ./aws/install`** — executa o script de instalação com privilégios de administrador, instalando o CLI globalmente em `/usr/local/bin/aws`.

---

## 2. Instalar o AWS CLI no macOS com Homebrew

```bash
brew install awscli
```

> **`brew install`** — utiliza o gerenciador de pacotes Homebrew para baixar e instalar o AWS CLI.
> **`awscli`** — nome do pacote oficial do AWS CLI no repositório do Homebrew.
> Após a instalação, o comando `aws` estará disponível globalmente no terminal.
> **Atenção:** execute apenas o passo referente ao seu sistema operacional (1 ou 2) antes de prosseguir.

---

## 3. Verificar a instalação

```bash
aws --version
```

> **`aws`** — é o executável principal do AWS CLI instalado no passo anterior.
> **`--version`** — exibe a versão atual do AWS CLI instalada, a versão do Python utilizado e o sistema operacional.
> A saída esperada é semelhante a: `aws-cli/2.x.x Python/3.x.x Linux/...`
> Use este comando para confirmar que a instalação foi concluída com sucesso antes de prosseguir.

---

## 4. Criar a Access Key e Secret Key no Console AWS

```bash
# Etapa realizada no Console AWS — acesse o endereço abaixo:
# https://console.aws.amazon.com/iam/home#/security_credentials
```

> **Navegue até:** Console AWS → menu do usuário (canto superior direito) → **Security credentials**.
> **Em "Access keys"**, clique em **"Create access key"**, selecione o caso de uso **"CLI"** e confirme.
> **Anote** o **Access Key ID** e o **Secret Access Key** exibidos — eles são mostrados apenas uma vez.
> Opcionalmente, faça o download do arquivo `.csv` como backup seguro das suas credenciais.

---

## 5. Configurar as credenciais no AWS CLI

```bash
aws configure
```

> **`aws configure`** — inicia o assistente interativo de configuração do AWS CLI.
> O comando solicitará quatro informações:
> - **AWS Access Key ID** — cole o Access Key ID criado no passo anterior.
> - **AWS Secret Access Key** — cole a Secret Access Key criada no passo anterior.
> - **Default region name** — informe a região padrão (ex: `us-east-1` ou `sa-east-1` para São Paulo).
> - **Default output format** — defina o formato de saída padrão (recomendado: `json`).
> As credenciais são salvas em `~/.aws/credentials` e as configurações em `~/.aws/config`.

---

## 6. Verificar a identidade configurada

```bash
aws sts get-caller-identity
```

> **`aws sts`** — acessa o serviço AWS Security Token Service via CLI.
> **`get-caller-identity`** — retorna informações sobre a identidade AWS associada às credenciais configuradas.
> A saída exibe o `UserId`, o `Account` (ID da conta AWS) e o `Arn` do usuário autenticado.
> Use este comando sempre que quiser confirmar com qual conta e usuário o AWS CLI está operando.

---

## 7. Listar os buckets S3

```bash
aws s3 ls
```

> **`aws s3`** — acessa o serviço Amazon S3 via AWS CLI.
> **`ls`** — lista todos os buckets S3 disponíveis na conta AWS autenticada.
> Se a conta não possuir buckets, o comando retorna uma lista vazia sem erros — isso confirma que a autenticação está funcionando corretamente.
> Para listar o conteúdo de um bucket específico, use: `aws s3 ls s3://nome-do-bucket`

---

## 8. Limpeza dos recursos

```bash
rm -f ~/.aws/credentials ~/.aws/config
```

> **`rm -f`** — remove os arquivos especificados sem solicitar confirmação (`-f` força a remoção silenciosa).
> **`~/.aws/credentials`** — arquivo que armazena o Access Key ID e o Secret Access Key configurados.
> **`~/.aws/config`** — arquivo que armazena a região padrão e o formato de saída configurados.
> **Importante:** antes de remover as credenciais locais, considere também desativar ou excluir a Access Key no Console AWS em `IAM → Security credentials → Access keys` para evitar uso indevido.

---

## 🎉 Finalizou o lab? Compartilhe!

Use o template abaixo para postar no LinkedIn — basta copiar, ajustar o que quiser e publicar!

```
☁️ Mais um lab concluído!

Hoje aprendi a instalar e configurar o AWS CLI usando a linha de comando.

✅ O que pratiquei:
• Instalei o AWS CLI no Linux e no macOS e validei a versão instalada
• Criei Access Key e Secret Key no Console AWS e configurei com aws configure
• Validei a autenticação com aws sts e listei buckets S3 com aws s3 ls

📖 Lab completo e gratuito:
https://github.com/iesodias/tech-challenge/blob/main/labs/aws/basico/03-instalando-aws-cli/README.md

🗂️ Repositório com todos os labs:
https://github.com/iesodias/tech-challenge

#AWS #Cloud #CloudComputing #TechChallenge #AprendizadoContínuo #DevOps
```

---
