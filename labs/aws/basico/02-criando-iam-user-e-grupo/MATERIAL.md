# Material de Estudo — AWS IAM (Usuários e Grupos)

> Resumo de apoio para o [Lab 02](README.md) | [Quiz](../../../../.github/ISSUE_TEMPLATE/quiz-aws-basico-02-criando-iam-user-e-grupo.yml)

---

## O que é AWS IAM?

**IAM** (Identity and Access Management) é o serviço da AWS que controla **quem** pode acessar **o quê** na sua conta. Com ele você cria usuários, grupos, funções (roles) e políticas de permissão (policies). O IAM é um serviço **global** — não está vinculado a nenhuma região específica — e é totalmente **gratuito**.

---

## Por que NÃO usar o usuário root?

- O **usuário root** possui acesso irrestrito a todos os recursos e configurações da conta, sem possibilidade de limitação
- Se as credenciais do root forem comprometidas, o atacante terá **controle total** da conta
- Não há **rastreabilidade individual** quando várias pessoas compartilham o root
- A AWS recomenda proteger o root com **MFA** (autenticação multifator) e usá-lo apenas para tarefas que exigem obrigatoriamente o root
- Para o dia a dia, crie **usuários IAM individuais** com apenas as permissões necessárias

---

## Conceitos-chave

- **Usuário IAM:** Identidade com credenciais próprias para acessar a AWS — pode ter acesso ao Console, à CLI ou a ambos
- **Grupo de usuários (User Group):** Conjunto de usuários IAM que compartilham as mesmas permissões. Políticas anexadas ao grupo são herdadas automaticamente por todos os membros
- **Política (Policy):** Documento JSON que define permissões — especifica quais ações são permitidas ou negadas em quais recursos
- **AdministratorAccess:** Política **gerenciada pela AWS** que concede acesso total a todos os serviços e recursos, similar ao root, mas com a vantagem de poder ser **revogada** a qualquer momento
- **Console sign-in URL:** URL específica para login de usuários IAM, no formato `https://<ACCOUNT_ID>.signin.aws.amazon.com/console` — diferente da URL de login do root
- **Serviço global:** O IAM não é vinculado a uma região — usuários, grupos e políticas criados ficam disponíveis em **todas as regiões** da AWS simultaneamente

---

## Resumo de configurações do lab

| Configuração | Valor usado no lab |
|---|---|
| Nome do grupo | Administradores |
| Política anexada ao grupo | AdministratorAccess (AWS managed policy) |
| Nome do usuário | admin-lab |
| Acesso ao Console | Habilitado |
| Método de permissão | Adicionar usuário ao grupo |
| Troca de senha no primeiro login | Desabilitada (apenas para o lab) |

---

## Boas práticas

- **Nunca use o root no dia a dia** — reserve-o apenas para tarefas obrigatórias como configurações de faturamento ou encerramento da conta
- **Gerencie permissões via grupos**, não diretamente nos usuários — isso centraliza o controle e facilita alterações em escala
- **Na limpeza, exclua o usuário antes do grupo** — remova os vínculos antes de deletar o contêiner de permissões
- **Não deixe usuários com permissões administrativas sem uso ativo** — mesmo sendo gratuito, recursos IAM ociosos representam risco de segurança

---

📝 [Responda o quiz para testar seu conhecimento](../../../../.github/ISSUE_TEMPLATE/quiz-aws-basico-02-criando-iam-user-e-grupo.yml)
