# Lab AWS – Criar um Usuário e Grupo IAM pelo Console AWS

Neste lab você vai aprender a criar um **Grupo IAM** com permissão de administrador e um **Usuário IAM** vinculado a esse grupo, usando o Console AWS. Você também vai entender por que **nunca deve usar o usuário root** no dia a dia — uma das práticas de segurança mais importantes da AWS.

---

## ⚠️ Por que NÃO usar o usuário root?

Quando você cria uma conta AWS, recebe um **usuário root** com acesso irrestrito a todos os recursos e configurações. Embora conveniente, usar o root no dia a dia é **extremamente perigoso** porque:

- **Não pode ter permissões limitadas:** O root sempre tem acesso total, sem restrições
- **Risco de danos irreversíveis:** Um comando errado pode excluir recursos críticos ou até encerrar a conta
- **Sem rastreabilidade individual:** Se várias pessoas usam o root, não há como saber quem fez cada ação
- **Alvo de ataques:** Credenciais root comprometidas dão controle total da conta

A **melhor prática** recomendada pela AWS é:

1. Proteger o root com **MFA** (autenticação multifator)
2. **Nunca usar o root** para tarefas do dia a dia
3. Criar **usuários IAM individuais** com apenas as permissões necessárias
4. Usar **grupos** para organizar permissões

É exatamente isso que faremos neste lab! 🔒

---

## Pré-requisitos

- Conta ativa na AWS (pode ser a [conta gratuita AWS Free Tier](https://aws.amazon.com/pt/free/))
- Navegador web atualizado (Chrome, Edge, Firefox)
- Acesso ao [Console AWS](https://console.aws.amazon.com)

---

## 1. Fazer login no Console AWS

Abra o navegador e acesse **[https://console.aws.amazon.com](https://console.aws.amazon.com)**. Insira seu e-mail (ou ID da conta), senha e conclua a autenticação. Após o login, você será direcionado à página inicial do Console AWS.

> **Console AWS (AWS Management Console)** é a interface web de gerenciamento da AWS. Para este lab, você fará login com a conta root (pois ainda não tem usuários IAM criados). Este será o **último lab** em que você usará o root — a partir de agora, você usará o usuário IAM que vamos criar.

---

## 2. Navegar até o serviço IAM

Na página inicial do console, localize a **barra de pesquisa** no topo da tela. Digite **"IAM"** e clique na opção **"IAM"** que aparece nos resultados sob a seção **Serviços**. Você será levado ao **IAM Dashboard** (painel de gerenciamento de identidades).

> **IAM (Identity and Access Management)** é o serviço da AWS que controla **quem** pode acessar **o quê** na sua conta. Com ele você cria usuários, grupos, funções (roles) e políticas de permissão (policies). O IAM é um serviço **global** — não está vinculado a nenhuma região específica — e é totalmente **gratuito**.

---

## 3. Criar o grupo de administradores

No painel do IAM, no menu de navegação à esquerda, clique em **"User groups"** (Grupos de usuários). Em seguida, clique no botão **"Create group"** (Criar grupo). Preencha as seguintes informações:

1. **User group name (Nome do grupo):** Digite **`Administradores`**
2. Na seção **"Attach permissions policies"** (Anexar políticas de permissão), pesquise por **`AdministratorAccess`** na barra de busca
3. Marque o **checkbox** ao lado da política **"AdministratorAccess"** (gerenciada pela AWS)
4. Clique no botão **"Create user group"** (Criar grupo de usuários) na parte inferior da página

> - **User group (Grupo de usuários):** É um conjunto de usuários IAM. Qualquer política (policy) anexada ao grupo é automaticamente aplicada a **todos os usuários** que fazem parte dele. Isso simplifica o gerenciamento de permissões — ao invés de configurar cada usuário individualmente, você configura o grupo uma vez.
> - **AdministratorAccess:** É uma política **gerenciada pela AWS** (AWS managed policy) que concede acesso total a todos os serviços e recursos da conta. Ela é equivalente às permissões do root, mas com a vantagem de poder ser **revogada** a qualquer momento. O ARN desta política é `arn:aws:iam::aws:policy/AdministratorAccess`.
> - **Por que criar o grupo antes do usuário?** Porque ao criar o usuário, já poderemos adicioná-lo diretamente ao grupo, herdando as permissões automaticamente.

---

## 4. Criar o usuário IAM

No menu de navegação à esquerda, clique em **"Users"** (Usuários). Em seguida, clique no botão **"Create user"** (Criar usuário). Preencha as seguintes informações:

1. **User name (Nome do usuário):** Digite o nome desejado, por exemplo: **`admin-lab`**
2. Marque a opção **"Provide user access to the AWS Management Console"** (Fornecer acesso ao Console AWS)
3. Selecione **"I want to create an IAM user"** (Quero criar um usuário IAM)
4. Em **"Console password"**, selecione **"Custom password"** (Senha personalizada) e defina uma senha forte
5. Desmarque a opção **"Users must create a new password at next sign-in"** (Usuário deve criar nova senha no próximo login) — para simplificar o lab
6. Clique em **"Next"** (Próximo)

> - **User name:** É o identificador único do usuário IAM dentro da conta. Será usado para fazer login no console. Recomenda-se usar nomes descritivos que identifiquem a pessoa ou função.
> - **Provide user access to the AWS Management Console:** Habilita o acesso via navegador web. Sem essa opção, o usuário só poderia acessar a AWS via CLI ou SDKs (acesso programático).
> - **Custom password:** Permite definir uma senha específica. Em ambiente de produção, o ideal é marcar a opção para o usuário trocar a senha no primeiro login.

---

## 5. Adicionar o usuário ao grupo Administradores

Na página **"Set permissions"** (Definir permissões):

1. Selecione a opção **"Add user to group"** (Adicionar usuário ao grupo)
2. Na lista de grupos, marque o **checkbox** ao lado do grupo **`Administradores`** que você criou no passo 3
3. Clique em **"Next"** (Próximo)
4. Na página **"Review and create"** (Revisar e criar), confira todas as informações:
   - Nome do usuário: `admin-lab`
   - Acesso ao console: Habilitado
   - Grupo: `Administradores` (com a política `AdministratorAccess`)
5. Clique em **"Create user"** (Criar usuário)

> - **Add user to group:** É a forma **recomendada pela AWS** para gerenciar permissões. Ao invés de anexar políticas diretamente ao usuário, você o adiciona a um grupo que já possui as permissões configuradas. Isso segue o princípio de **gerenciamento centralizado** — se precisar alterar permissões, basta modificar o grupo e todos os membros serão afetados.
> - **Herança de permissões:** O usuário `admin-lab` herdará automaticamente a política `AdministratorAccess` do grupo `Administradores`, recebendo acesso total aos serviços da AWS.

---

## 6. Salvar as informações de login

Após a criação do usuário, você verá a página de **sucesso** com as informações de acesso. **Salve estas informações agora**, pois algumas não poderão ser exibidas novamente:

1. Anote a **URL de login do console** (Console sign-in URL) — ela segue o formato: `https://<ACCOUNT_ID>.signin.aws.amazon.com/console`
2. Anote o **nome do usuário** (`admin-lab`)
3. A **senha** é a que você definiu no passo anterior
4. Clique em **"Return to users list"** (Retornar à lista de usuários)

> - **Console sign-in URL:** É o link específico para login de usuários IAM da sua conta. Ele inclui o **ID da conta AWS** (ou um alias, se configurado). Usuários IAM **não usam** a mesma URL de login do root — eles precisam desta URL específica ou do ID da conta.
> - **Dica de segurança:** Em ambiente de produção, configure um **Account Alias** (apelido da conta) para facilitar a URL de login e evitar expor o ID numérico da conta.

---

## 7. Testar o login com o novo usuário

Para validar que tudo está funcionando corretamente:

1. Abra uma **janela anônima/privada** do navegador (para não conflitar com a sessão root atual)
2. Acesse a **URL de login do console** que você anotou no passo anterior
3. Insira o **User name:** `admin-lab`
4. Insira a **senha** definida no passo 4
5. Clique em **"Sign in"** (Entrar)
6. Após o login, navegue até alguns serviços (S3, EC2, IAM) para confirmar que o acesso está funcionando

> Este teste é fundamental para garantir que o usuário está corretamente configurado. Se o login falhar, verifique: (1) se a URL de login está correta, (2) se o nome do usuário está exato (é case-sensitive) e (3) se a senha está correta. Após confirmar que funciona, **a partir de agora use sempre este usuário IAM** para acessar o Console AWS, e reserve o root apenas para tarefas que exigem obrigatoriamente o root (como alterar configurações de faturamento ou encerrar a conta).

---

## 8. Limpeza dos recursos

Para manter sua conta organizada, vamos excluir o usuário e o grupo criados neste lab. **Faça login com o root** (ou com outra conta com permissão) para executar a limpeza:

**Passo A — Excluir o usuário IAM:**

1. No Console AWS, navegue até **IAM** > **"Users"** (Usuários)
2. Selecione o **botão de opção** (radio button) ao lado do usuário **`admin-lab`**
3. Clique no botão **"Delete"** (Excluir)
4. Na caixa de confirmação, digite o nome do usuário **`admin-lab`** e clique em **"Delete user"** (Excluir usuário)

**Passo B — Excluir o grupo de usuários:**

1. No menu à esquerda, clique em **"User groups"** (Grupos de usuários)
2. Selecione o **botão de opção** (radio button) ao lado do grupo **`Administradores`**
3. Clique no botão **"Delete"** (Excluir)
4. Na caixa de confirmação, digite o nome do grupo **`Administradores`** e clique em **"Delete"** (Excluir)

> É importante excluir o usuário **antes** do grupo. Embora a AWS permita excluir o grupo mesmo com membros, a boa prática é remover os vínculos primeiro. O IAM é um serviço gratuito, então não há custos associados a usuários e grupos — mas manter recursos de lab ativos pode gerar confusão e riscos de segurança. **Nunca deixe usuários com permissões administrativas sem uso ativo na sua conta.**

---

## 🎉 Finalizou o lab? Compartilhe!

Use o template abaixo para postar no LinkedIn — basta copiar, ajustar o que quiser e publicar!

```
☁️ Mais um lab concluído!

Hoje aprendi a criar um Usuário e Grupo IAM com permissão de administrador usando o Console AWS.

✅ O que pratiquei:
• Criar um Grupo IAM com a política AdministratorAccess e adicionar um usuário a ele
• Configurar acesso ao Console AWS para um usuário IAM sem usar o root
• Entender por que nunca usar o usuário root no dia a dia e limpar os recursos ao final

📖 Lab completo e gratuito:
https://github.com/iesodias/tech-challenge/blob/main/labs/aws/basico/02-criando-iam-user-e-grupo/README.md

🗂️ Repositório com todos os labs:
https://github.com/iesodias/tech-challenge

#AWS #Cloud #CloudComputing #TechChallenge #AprendizadoContínuo #DevOps
```
