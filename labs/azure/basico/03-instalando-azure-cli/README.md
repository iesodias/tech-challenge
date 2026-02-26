# Lab Azure – Instalar e Configurar o Azure CLI

Neste lab você vai instalar o Azure CLI na sua máquina e realizar os primeiros comandos para autenticar e explorar sua conta Azure. O Azure CLI é a ferramenta de linha de comando oficial da Microsoft para gerenciar recursos Azure de forma rápida e automatizável.

---

## Pré-requisitos

- Conta Azure ativa (gratuita ou paga)
- Acesso ao terminal (Linux, macOS ou Windows)
- Conexão com a internet
- Para macOS: Homebrew instalado (`https://brew.sh`)

---

## 1. Instalar o Azure CLI no Linux (Ubuntu/Debian)

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

> **`curl -sL`** — faz o download silencioso (`-s`) do script de instalação, seguindo redirecionamentos (`-L`).
> **`| sudo bash`** — passa o script baixado diretamente para execução com privilégios de administrador.
> Este comando instala automaticamente todas as dependências e a versão mais recente do Azure CLI.

---

## 2. Instalar o Azure CLI no macOS com Homebrew

```bash
brew install azure-cli
```

> **`brew install`** — utiliza o gerenciador de pacotes Homebrew para baixar, compilar e instalar o Azure CLI.
> **`azure-cli`** — nome do pacote oficial do Azure CLI no repositório do Homebrew.
> Após a instalação, o comando `az` estará disponível globalmente no terminal.

---

## 3. Verificar a versão instalada

```bash
az --version
```

> **`az`** — é o executável principal do Azure CLI.
> **`--version`** — exibe a versão atual do Azure CLI instalada, as versões das extensões e as dependências do Python.
> Use este comando para confirmar que a instalação foi concluída com sucesso.

---

## 4. Fazer login no Azure

```bash
az login
```

> **`az login`** — abre automaticamente o navegador padrão para autenticação interativa na conta Microsoft Azure.
> Após inserir suas credenciais no navegador, o terminal exibirá uma lista das assinaturas disponíveis associadas à sua conta.
> Em ambientes sem interface gráfica, use `az login --use-device-code` para autenticação via código.

---

## 5. Listar as assinaturas disponíveis

```bash
az account list --output table
```

> **`az account list`** — lista todas as assinaturas Azure associadas à conta autenticada.
> **`--output table`** — formata a saída em uma tabela legível, exibindo nome, ID e estado de cada assinatura.
> Guarde o valor da coluna `SubscriptionId` da assinatura que deseja usar.

---

## 6. Definir a assinatura padrão

```bash
az account set --subscription "<ID_DA_ASSINATURA>"
```

> **`az account set`** — define qual assinatura será usada por padrão em todos os comandos seguintes.
> **`--subscription`** — aceita o ID (GUID) ou o nome da assinatura desejada.
> Substitua `<ID_DA_ASSINATURA>` pelo valor obtido no passo anterior.

---

## 7. Verificar a conta ativa

```bash
az account show
```

> **`az account show`** — exibe os detalhes completos da assinatura atualmente ativa, incluindo `id`, `name`, `tenantId` e `user`.
> Use este comando para confirmar que a assinatura correta está configurada antes de criar recursos.

---

## 8. Limpeza dos recursos

```bash
az logout
```

> **`az logout`** — encerra a sessão autenticada e remove o token de acesso do cache local.
> Como este lab não cria recursos no Azure, basta fazer logout para finalizar com segurança.
> Para remover completamente as credenciais armazenadas, execute também: `az account clear`

---

## 🎉 Finalizou o lab? Compartilhe!

Use o template abaixo para postar no LinkedIn — basta copiar, ajustar o que quiser e publicar!

```
🔷 Mais um lab concluído!

Hoje aprendi a instalar e configurar o Azure CLI usando a linha de comando.

✅ O que pratiquei:
• Instalei o Azure CLI no Linux com curl e no macOS com Homebrew
• Autentiquei no Azure com az login e gerenciei assinaturas com az account
• Aprendi boas práticas como fazer logout e limpar credenciais locais

📖 Lab completo e gratuito:
https://github.com/iesodias/tech-challenge/blob/main/labs/azure/basico/03-instalando-azure-cli/README.md

🗂️ Repositório com todos os labs:
https://github.com/iesodias/tech-challenge

#Azure #Cloud #CloudComputing #TechChallenge #AprendizadoContínuo #DevOps
```
