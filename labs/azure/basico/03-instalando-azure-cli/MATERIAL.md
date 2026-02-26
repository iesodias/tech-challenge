# Material de Estudo — Azure CLI

> Resumo de apoio para o [Lab 03](README.md) | [Quiz](../../../../.github/ISSUE_TEMPLATE/azure-quiz-basico-03-instalando-azure-cli.yml)

---

## O que é Azure CLI?

O **Azure CLI** (Command-Line Interface) é a ferramenta oficial de linha de comando da Microsoft para criar, gerenciar e automatizar recursos no Azure. Funciona em Linux, macOS e Windows, e é distribuída como o executável `az`. É a alternativa ao portal web para fluxos automatizáveis e scripting.

---

## Conceitos-chave

- **`az`:** Executável principal do Azure CLI — todos os comandos começam com `az`
- **`az --version`:** Verifica a versão instalada do CLI, das extensões e das dependências Python
- **`az login`:** Autentica de forma interativa abrindo o navegador padrão para credenciais Microsoft
- **`az login --use-device-code`:** Alternativa para ambientes sem interface gráfica — exibe um código a ser inserido em outro dispositivo
- **`az account list`:** Lista todas as assinaturas vinculadas à conta autenticada
- **`az account set --subscription`:** Define a assinatura padrão para os comandos seguintes (aceita ID ou nome)
- **`az logout`:** Encerra a sessão e remove o token de acesso do cache local
- **`az account clear`:** Remove completamente todas as credenciais armazenadas localmente

---

## Resumo de configurações do lab

| Etapa | Comando principal |
|---|---|
| Instalação Linux | `curl -sL https://aka.ms/InstallAzureCLIDeb \| sudo bash` |
| Instalação macOS | `brew install azure-cli` |
| Verificar instalação | `az --version` |
| Autenticar | `az login` |
| Listar assinaturas | `az account list --output table` |
| Definir assinatura | `az account set --subscription "<ID>"` |
| Confirmar assinatura ativa | `az account show` |
| Encerrar sessão | `az logout` |

---

## Boas práticas

- **Sempre verifique a versão após instalar** — confirma que o executável `az` está no PATH e funcional
- **Use `--output table`** para leitura humana e `--output json` em scripts que precisam parsear a saída
- **Defina a assinatura explicitamente** com `az account set` antes de criar recursos — evita provisionar em ambiente errado
- **Faça logout ao terminar** — especialmente em máquinas compartilhadas; use `az account clear` para remover todas as credenciais

---

📝 [Responda o quiz para testar seu conhecimento](../../../../.github/ISSUE_TEMPLATE/azure-quiz-basico-03-instalando-azure-cli.yml)
