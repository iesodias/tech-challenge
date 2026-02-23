# Material de Estudo — Storage Account

> Resumo de apoio para o [Lab 02](README.md) | [Quiz](../../../../.github/ISSUE_TEMPLATE/quiz-azure-basico-02-criando-storage-account.yml)

---

## O que é Storage Account?

**Storage Account** (Conta de Armazenamento) é o recurso do Azure que fornece um namespace exclusivo para armazenar dados na nuvem. Ela suporta quatro tipos de serviço: **Blob Storage**, **File Storage**, **Queue Storage** e **Table Storage**. O nome da conta compõe a URL pública de acesso aos dados.

---

## Conceitos-chave

- **Blob Storage:** Armazenamento de objetos (arquivos, imagens, backups) — acessível via HTTP/HTTPS
- **File Storage:** Compartilhamentos de arquivos via protocolo SMB, acessíveis como unidades de rede
- **Queue Storage:** Filas de mensagens para comunicação assíncrona entre componentes de aplicações
- **Table Storage:** Armazenamento NoSQL de chave-valor para dados estruturados sem esquema fixo
- **Nome globalmente único:** O nome da Storage Account faz parte da URL do endpoint (ex: `https://nomedaconta.blob.core.windows.net/`), por isso deve ser único em todo o Azure
- **Redundância LRS:** Mantém **3 cópias** dos dados no mesmo data center — opção mais econômica
- **Performance Standard vs Premium:** Standard usa HDD (maioria dos cenários); Premium usa SSD (baixa latência)

---

## Resumo de configurações do lab

| Configuração | Valor usado no lab |
|---|---|
| Resource Group | `lab-rg-01` |
| Nome | `labstorage01<iniciais>` (globalmente único) |
| Região | Brazil South |
| Performance | Standard |
| Redundância | LRS (Locally-redundant storage) |
| Tags | `Ambiente: Lab`, `Projeto: TechChallenge` |

---

## Boas práticas

- **Escolha a redundância adequada** — LRS é suficiente para labs, mas ambientes de produção geralmente exigem GRS ou ZRS
- **Use nomes descritivos** — o nome é permanente e visível nas URLs de acesso
- **Associe a um Resource Group** de lab — facilita a limpeza e organização
- **A exclusão é irreversível** — todos os dados (blobs, arquivos, filas e tabelas) são permanentemente removidos ao excluir a conta

---

📝 [Responda o quiz para testar seu conhecimento](../../../../.github/ISSUE_TEMPLATE/quiz-azure-basico-02-criando-storage-account.yml)
