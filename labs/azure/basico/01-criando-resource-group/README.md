# Lab Azure – Criar um Resource Group pelo Portal Azure

Neste lab você vai aprender a criar seu primeiro **Resource Group** (Grupo de Recursos) usando o Portal Azure. O Resource Group é o bloco fundamental de organização no Azure — todo recurso precisa pertencer a um.

---

## Pré-requisitos

- Conta ativa no Microsoft Azure (pode ser a [conta gratuita](https://azure.microsoft.com/pt-br/free/))
- Navegador web atualizado (Chrome, Edge, Firefox)
- Acesso ao [Portal Azure](https://portal.azure.com)

---

## 1. Fazer login no Portal Azure

Abra o navegador e acesse **[https://portal.azure.com](https://portal.azure.com)**. Insira seu e-mail e senha da conta Microsoft associada à sua assinatura Azure. Após autenticar, você será direcionado à página inicial do portal.

> **Portal Azure** é a interface web de gerenciamento do Azure. Por ele você pode criar, configurar, monitorar e excluir todos os recursos da sua conta. A página inicial mostra um painel (dashboard) com atalhos e recursos recentes.

---

## 2. Navegar até Resource Groups

Na página inicial do portal, localize a **barra de pesquisa** no topo da tela. Digite **"Resource groups"** e clique na opção **"Resource groups"** que aparece nos resultados sob a seção **Serviços**.

> **Resource Group (Grupo de Recursos)** é um contêiner lógico que agrupa recursos relacionados no Azure (VMs, bancos de dados, contas de armazenamento, etc.). Ele facilita o gerenciamento, o controle de acesso e a organização de custos. Todos os recursos dentro de um Resource Group podem ser gerenciados e excluídos como uma unidade.

---

## 3. Iniciar a criação de um novo Resource Group

Na página de Resource Groups, clique no botão **"+ Create"** (ou **"+ Criar"**) localizado no canto superior esquerdo da tela. Isso abrirá o formulário de criação de um novo Resource Group.

> O botão **"+ Create"** é o ponto de partida para criar qualquer recurso no Azure. No contexto de Resource Groups, ele abre um formulário com abas (Basics, Tags, Review + Create) onde você preencherá as informações necessárias.

---

## 4. Preencher as informações básicas

Na aba **"Basics"** (Básico), preencha os seguintes campos:

- **Subscription (Assinatura):** Selecione a assinatura Azure que você deseja usar (ex: "Azure subscription 1" ou "Free Trial")
- **Resource group (Grupo de recursos):** Digite **`lab-rg-01`**
- **Region (Região):** Selecione **`(South America) Brazil South`**

> - **Subscription (Assinatura):** É o contrato de cobrança do Azure. Todos os custos dos recursos criados serão vinculados a essa assinatura. Se você tem uma conta gratuita, verá algo como "Free Trial" ou "Azure subscription 1".
> - **Resource group name:** O nome deve ser único dentro da sua assinatura. Usamos `lab-rg-01` seguindo a convenção de nomenclatura para labs.
> - **Region (Região):** Define onde os **metadados** do Resource Group serão armazenados. Escolhemos **Brazil South** (São Paulo) por ser a região mais próxima do Brasil, resultando em menor latência. Os recursos dentro do grupo podem ser criados em regiões diferentes.

---

## 5. Adicionar tags ao Resource Group

Clique na aba **"Tags"** no topo do formulário. Adicione as seguintes tags preenchendo os campos **Name** (Nome) e **Value** (Valor):

| Name (Nome) | Value (Valor) |
|---|---|
| `Ambiente` | `Lab` |
| `Projeto` | `TechChallenge` |

Para cada tag, preencha o campo **Name**, depois o campo **Value** e clique na linha seguinte para adicionar a próxima.

> **Tags** são pares de chave-valor que você pode atribuir aos recursos do Azure para organizá-los logicamente. Elas são fundamentais para:
> - **Organização:** Categorizar recursos por ambiente (Dev, Staging, Produção), projeto ou equipe
> - **Gestão de custos:** Filtrar e agrupar custos por tag nos relatórios de faturamento
> - **Automação:** Identificar recursos em scripts e políticas
>
> Neste lab, usamos `Ambiente: Lab` para indicar que é um recurso de laboratório e `Projeto: TechChallenge` para associar ao projeto.

---

## 6. Revisar e criar o Resource Group

Clique na aba **"Review + create"** (Revisar + criar). O Azure irá validar as informações preenchidas. Confira os dados exibidos na tela:

- **Subscription:** Sua assinatura selecionada
- **Resource group:** `lab-rg-01`
- **Region:** `Brazil South`
- **Tags:** `Ambiente: Lab` e `Projeto: TechChallenge`

Se tudo estiver correto e a validação mostrar **"Validation passed"** (Validação aprovada), clique no botão **"Create"** (Criar) na parte inferior da página.

> A etapa de **Review + create** é uma validação automática do Azure. Ela verifica se todos os campos obrigatórios foram preenchidos e se não há conflitos (como nomes duplicados). Somente após a validação bem-sucedida o botão "Create" será habilitado. Após clicar em "Create", o Azure provisiona o Resource Group em poucos segundos.

---

## 7. Verificar o Resource Group criado

Após a criação, você será redirecionado para a página do Resource Group ou verá uma notificação de sucesso. Para confirmar:

1. Clique no ícone de **sino (Notificações)** no canto superior direito do portal
2. Veja a mensagem **"Resource group created"** (Grupo de recursos criado)
3. Clique em **"Go to resource group"** (Ir para o grupo de recursos) para abrir o `lab-rg-01`

Na página do Resource Group, observe as informações: nome, assinatura, região e as tags que você configurou.

> Após criar qualquer recurso no Azure, é uma boa prática verificar se ele foi provisionado corretamente. O **painel de notificações** (ícone de sino) mostra o histórico de todas as operações recentes, incluindo status de sucesso ou falha.

---

## 8. Limpeza dos recursos

Para evitar qualquer custo ou manter sua assinatura organizada, vamos excluir o Resource Group criado:

1. Na barra de pesquisa do portal, digite **"Resource groups"** e clique no resultado
2. Na lista de Resource Groups, localize o **`lab-rg-01`**
3. Clique no nome **`lab-rg-01`** para abrir a página do grupo
4. Clique no botão **"Delete resource group"** (Excluir grupo de recursos) no topo da página
5. No campo de confirmação, digite o nome do Resource Group: **`lab-rg-01`**
6. Clique no botão **"Delete"** (Excluir) na parte inferior

> Ao excluir um Resource Group, **todos os recursos dentro dele são excluídos automaticamente**. Por isso, Resource Groups são muito úteis para labs e ambientes temporários — basta excluir o grupo para limpar tudo de uma vez. O Azure pede que você digite o nome do grupo como confirmação para evitar exclusões acidentais. A exclusão pode levar alguns minutos para ser concluída.

---

## 🎉 Finalizou o lab? Compartilhe!

Use o template abaixo para postar no LinkedIn — basta copiar, ajustar o que quiser e publicar!

```
🔷 Mais um lab concluído!

Hoje aprendi a criar um Resource Group usando o Portal Azure.

✅ O que pratiquei:
• Criar um Resource Group na região Brazil South e adicionar tags de organização
• Entender que o Resource Group é o contêiner lógico fundamental do Azure
• Excluir o Resource Group (e todos os recursos dentro dele) ao final do lab

📖 Lab completo e gratuito:
https://github.com/iesodias/tech-challenge/blob/main/labs/azure/basico/01-criando-resource-group/README.md

🗂️ Repositório com todos os labs:
https://github.com/iesodias/tech-challenge

#Azure #Cloud #CloudComputing #TechChallenge #AprendizadoContínuo #DevOps
```
