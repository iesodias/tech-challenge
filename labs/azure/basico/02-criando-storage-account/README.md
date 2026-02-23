# Lab Azure – Criar uma Storage Account pelo Portal Azure

Neste lab você vai aprender a criar sua primeira **Storage Account** (Conta de Armazenamento) usando o Portal Azure. A Storage Account é o recurso fundamental de armazenamento no Azure, permitindo guardar blobs, arquivos, filas e tabelas.

---

## Pré-requisitos

- Conta ativa no Microsoft Azure (pode ser a [conta gratuita](https://azure.microsoft.com/pt-br/free/))
- Navegador web atualizado (Chrome, Edge, Firefox)
- Acesso ao [Portal Azure](https://portal.azure.com)
- Um Resource Group já criado (ex: `lab-rg-01`) — caso não tenha, siga o [Lab 01](../01-criando-resource-group/README.md)

---

## 1. Fazer login no Portal Azure

Abra o navegador e acesse **[https://portal.azure.com](https://portal.azure.com)**. Insira seu e-mail e senha da conta Microsoft associada à sua assinatura Azure. Após autenticar, você será direcionado à página inicial do portal.

> **Portal Azure** é a interface web de gerenciamento do Azure. Por ele você pode criar, configurar, monitorar e excluir todos os recursos da sua conta. A página inicial mostra um painel (dashboard) com atalhos e recursos recentes.

---

## 2. Navegar até Storage Accounts

Na página inicial do portal, localize a **barra de pesquisa** no topo da tela. Digite **"Storage accounts"** e clique na opção **"Storage accounts"** que aparece nos resultados sob a seção **Serviços**.

> **Storage Account (Conta de Armazenamento)** é o recurso do Azure que fornece um namespace exclusivo para armazenar dados. Ela suporta quatro tipos de serviços: **Blob Storage** (objetos/arquivos), **File Storage** (compartilhamentos SMB), **Queue Storage** (filas de mensagens) e **Table Storage** (dados NoSQL). O nome da Storage Account faz parte da URL de acesso aos dados, por exemplo: `https://labstorage01.blob.core.windows.net/`.

---

## 3. Iniciar a criação de uma nova Storage Account

Na página de Storage Accounts, clique no botão **"+ Create"** (ou **"+ Criar"**) localizado no canto superior esquerdo da tela. Isso abrirá o formulário de criação com várias abas de configuração.

> O botão **"+ Create"** inicia o assistente de criação de uma Storage Account. O formulário é dividido em abas: **Basics** (configurações obrigatórias), **Advanced** (opções avançadas), **Networking** (rede), **Data protection** (proteção de dados), **Encryption** (criptografia), **Tags** e **Review + create**. Para este lab, vamos preencher apenas as abas essenciais.

---

## 4. Preencher as informações básicas

Na aba **"Basics"** (Básico), preencha os seguintes campos:

- **Subscription (Assinatura):** Selecione a sua assinatura Azure (ex: "Free Trial" ou "Azure subscription 1")
- **Resource group (Grupo de recursos):** Selecione **`lab-rg-01`** (criado no Lab 01)
- **Storage account name (Nome da conta de armazenamento):** Digite **`labstorage01<seus-iniciais>`** (ex: `labstorage01abc`) — o nome deve ser **globalmente único**, ter entre 3 e 24 caracteres, e usar apenas **letras minúsculas e números**
- **Region (Região):** Selecione **`(South America) Brazil South`**
- **Performance (Desempenho):** Mantenha selecionado **`Standard`**
- **Redundancy (Redundância):** Selecione **`Locally-redundant storage (LRS)`**

> - **Subscription (Assinatura):** É o contrato de cobrança onde os custos da Storage Account serão registrados.
> - **Resource group:** Associa a Storage Account a um grupo de recursos existente. Isso facilita o gerenciamento e a organização dos recursos relacionados.
> - **Storage account name:** O nome deve ser **globalmente único** em todo o Azure, pois ele compõe a URL pública de acesso (ex: `https://labstorage01abc.blob.core.windows.net/`). Aceita apenas letras minúsculas e números, sem hífens ou caracteres especiais.
> - **Region (Região):** Define o data center onde os dados serão fisicamente armazenados. Escolhemos **Brazil South** (São Paulo) para menor latência no Brasil.
> - **Performance:** **Standard** usa discos HDD e é indicado para a maioria dos cenários. **Premium** usa discos SSD e é ideal para cargas de trabalho que exigem baixa latência.
> - **Redundancy (Redundância):** Define como os dados são replicados para proteção contra falhas. **LRS (Locally-redundant storage)** mantém 3 cópias dos dados no mesmo data center — é a opção mais barata e suficiente para labs.

---

## 5. Adicionar tags à Storage Account

Clique na aba **"Tags"** no topo do formulário. Adicione as seguintes tags preenchendo os campos **Name** (Nome) e **Value** (Valor):

| Name (Nome) | Value (Valor) |
|---|---|
| `Ambiente` | `Lab` |
| `Projeto` | `TechChallenge` |

Para cada tag, preencha o campo **Name**, depois o campo **Value** e clique na linha seguinte para adicionar a próxima.

> **Tags** são pares de chave-valor que ajudam a organizar recursos no Azure. Elas permitem categorizar por ambiente, projeto ou equipe, facilitam a filtragem de custos nos relatórios de faturamento e são úteis para automação com políticas. Neste lab, usamos `Ambiente: Lab` e `Projeto: TechChallenge` para identificar o recurso.

---

## 6. Revisar e criar a Storage Account

Clique na aba **"Review + create"** (Revisar + criar). O Azure executará uma validação automática das configurações. Confira os dados exibidos na tela:

- **Subscription:** Sua assinatura selecionada
- **Resource group:** `lab-rg-01`
- **Storage account name:** O nome que você escolheu
- **Region:** `Brazil South`
- **Performance:** `Standard`
- **Redundancy:** `LRS`
- **Tags:** `Ambiente: Lab` e `Projeto: TechChallenge`

Se a validação mostrar **"Validation passed"** (Validação aprovada), clique no botão **"Create"** (Criar) na parte inferior da página.

> A etapa de **Review + create** valida todas as configurações antes de provisionar o recurso. O Azure verifica se o nome é único, se a região está disponível e se não há conflitos. Após clicar em "Create", o **deployment** (implantação) será iniciado — a criação de uma Storage Account geralmente leva de 30 segundos a 2 minutos.

---

## 7. Verificar a Storage Account criada

Após a criação, você verá a mensagem **"Your deployment is complete"** (Sua implantação foi concluída). Para verificar:

1. Clique no botão **"Go to resource"** (Ir para o recurso) na tela de implantação
2. Na página da Storage Account, observe as informações: **nome**, **região**, **tipo de desempenho**, **redundância** e os **endpoints** (URLs de acesso)
3. No menu lateral esquerdo, clique em **"Endpoints"** para ver as URLs de cada serviço (Blob, File, Queue, Table)

> Cada Storage Account recebe **endpoints exclusivos** baseados no nome escolhido. Por exemplo: `https://labstorage01abc.blob.core.windows.net/` para Blob Storage. Esses endpoints são as URLs que aplicações usam para acessar os dados armazenados. Verificar o recurso criado é uma boa prática para confirmar que tudo foi provisionado corretamente.

---

## 8. Limpeza dos recursos

Para evitar custos desnecessários, vamos excluir a Storage Account criada:

1. Na barra de pesquisa do portal, digite **"Storage accounts"** e clique no resultado
2. Na lista de Storage Accounts, localize a conta que você criou
3. Clique no nome da Storage Account para abrir a página do recurso
4. Clique no botão **"Delete"** (Excluir) no topo da página
5. No campo de confirmação, digite o **nome da Storage Account**
6. Clique no botão **"Delete"** (Excluir) para confirmar

> A exclusão de uma Storage Account é **irreversível** — todos os dados armazenados (blobs, arquivos, filas e tabelas) serão **permanentemente removidos**. O Azure pede que você digite o nome do recurso como confirmação para evitar exclusões acidentais. Se a Storage Account estiver dentro de um Resource Group de lab que você também vai excluir, basta deletar o Resource Group inteiro — todos os recursos dentro dele serão removidos automaticamente (exclusão em cascata).

---

## 🎉 Finalizou o lab? Compartilhe!

Use o template abaixo para postar no LinkedIn — basta copiar, ajustar o que quiser e publicar!

```
🔷 Mais um lab concluído!

Hoje aprendi a criar uma Storage Account e um Container de blobs usando o Portal Azure.

✅ O que pratiquei:
• Criar uma Storage Account com redundância LRS na região Brazil South
• Criar um container privado e fazer upload de arquivos como blobs
• Excluir todos os recursos ao final para evitar custos desnecessários

📖 Lab completo e gratuito:
https://github.com/iesodias/tech-challenge/blob/main/labs/azure/basico/02-criando-storage-account/README.md

🗂️ Repositório com todos os labs:
https://github.com/iesodias/tech-challenge

#Azure #Cloud #CloudComputing #TechChallenge #AprendizadoContínuo #DevOps
```
