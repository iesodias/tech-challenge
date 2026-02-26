# Material de Estudo — AWS CLI

> Resumo de apoio para o [Lab 03](README.md)

---

## O que é o AWS CLI?

**AWS CLI** (Command Line Interface) é a ferramenta oficial da Amazon para interagir com todos os serviços da AWS diretamente pelo terminal. Com ele, é possível criar, listar, modificar e excluir recursos sem precisar acessar o Console Web — o que é essencial para automação, scripts e pipelines de CI/CD.

O AWS CLI v2 é a versão atual e recomendada. Ele é escrito em Python, mas distribuído como um binário compilado e não requer Python instalado separadamente na maioria dos sistemas.

---

## Conceitos-chave

- **Access Key ID:** Identificador público da credencial de acesso programático de um usuário IAM. Funciona como um "usuário" em um par de login
- **Secret Access Key:** Chave secreta associada ao Access Key ID. Funciona como a "senha" — nunca deve ser exposta ou compartilhada
- **`aws configure`:** Comando interativo que salva as credenciais e configurações regionais nos arquivos `~/.aws/credentials` e `~/.aws/config`
- **Perfis (profiles):** O AWS CLI suporta múltiplos perfis nomeados, permitindo alternar entre diferentes contas ou usuários sem reconfigurar
- **STS (Security Token Service):** Serviço que emite credenciais temporárias e permite verificar a identidade ativa — o comando `get-caller-identity` é amplamente usado para validar configurações
- **Região padrão:** Define em qual região geográfica da AWS os comandos serão executados por padrão quando nenhuma região for especificada explicitamente

---

## Arquivos de configuração do AWS CLI

Após executar `aws configure`, dois arquivos são criados automaticamente:

| Arquivo | Conteúdo |
|---|---|
| `~/.aws/credentials` | Access Key ID e Secret Access Key |
| `~/.aws/config` | Região padrão e formato de saída |

**Exemplo de `~/.aws/credentials`:**
```ini
[default]
aws_access_key_id = AKIAIOSFODNN7EXAMPLE
aws_secret_access_key = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```

**Exemplo de `~/.aws/config`:**
```ini
[default]
region = us-east-1
output = json
```

---

## Formatos de saída disponíveis

O AWS CLI suporta quatro formatos de saída configuráveis:

| Formato | Descrição |
|---|---|
| `json` | Padrão — estruturado e compatível com scripts |
| `yaml` | Legível para humanos, útil para inspeção manual |
| `table` | Visual em tabela, bom para leitura no terminal |
| `text` | Texto simples separado por tabulações, útil com `awk` e `grep` |

---

## Regiões AWS mais usadas no Brasil

| Região | Nome |
|---|---|
| `sa-east-1` | América do Sul (São Paulo) |
| `us-east-1` | Leste dos EUA (Norte da Virgínia) |
| `us-west-2` | Oeste dos EUA (Oregon) |

Para projetos com usuários no Brasil, prefira `sa-east-1` para menor latência.

---

## Boas práticas de segurança com Access Keys

- **Nunca versione credenciais no Git** — adicione `~/.aws/` ao `.gitignore` de projetos locais e nunca coloque Access Keys em código-fonte
- **Evite criar Access Keys para o usuário root** — crie um usuário IAM com permissões mínimas necessárias (princípio do menor privilégio)
- **Rotacione as Access Keys periodicamente** — desative chaves antigas após criar novas no Console AWS (`IAM → Security credentials → Access keys`)
- **Prefira roles IAM em ambientes de nuvem** — para EC2, Lambda, ECS e demais serviços, use Instance Profiles/Roles em vez de Access Keys fixas
- **Habilite MFA para o usuário IAM** — adiciona uma camada extra de proteção à conta
- **Desative imediatamente chaves comprometidas** — se suspeitar que uma chave foi exposta, desative e exclua no Console antes de qualquer outra ação
- **Use o AWS Secrets Manager ou variáveis de ambiente** em pipelines — evite salvar credenciais em arquivos de configuração em ambientes compartilhados

---

## Comandos úteis adicionais

**Verificar identidade ativa:**
```bash
aws sts get-caller-identity
```

**Usar perfil alternativo:**
```bash
aws s3 ls --profile nome-do-perfil
```

**Definir região pontualmente (sem alterar o padrão):**
```bash
aws s3 ls --region sa-east-1
```

**Verificar a configuração atual:**
```bash
aws configure list
```

**Configurar um perfil nomeado:**
```bash
aws configure --profile meu-perfil
```

**Listar todos os perfis configurados:**
```bash
aws configure list-profiles
```

**Testar acesso ao S3 sem criar recursos:**
```bash
aws s3 ls
```

**Obter ajuda de qualquer comando:**
```bash
aws s3 help
aws sts get-caller-identity help
```

---

## Erros comuns e como resolver

| Erro | Causa | Solução |
|---|---|---|
| `command not found: aws` | AWS CLI não está instalado ou não está no PATH | Reinstale seguindo o passo 1 ou 2 do lab e reinicie o terminal |
| `Unable to locate credentials` | `aws configure` não foi executado | Execute `aws configure` e informe as credenciais |
| `InvalidClientTokenId` | Access Key ID inválido ou deletado | Verifique o Key ID no Console AWS (`IAM → Security credentials`) |
| `SignatureDoesNotMatch` | Secret Access Key incorreta | Recrie a Access Key no Console e reconfigure com `aws configure` |
| `AccessDenied` | Usuário IAM sem permissão para o recurso | Verifique as policies anexadas ao usuário no Console IAM |
| `AuthFailure` | Credenciais expiradas (token temporário) | Gere novas credenciais ou assuma um novo role com `aws sts assume-role` |
| `NoRegionError` | Nenhuma região configurada | Execute `aws configure` e defina uma região padrão (ex: `us-east-1`) |

---

## Variáveis de ambiente como alternativa ao `aws configure`

O AWS CLI também aceita credenciais via variáveis de ambiente, útil em pipelines de CI/CD:

```bash
export AWS_ACCESS_KEY_ID="AKIAIOSFODNN7EXAMPLE"
export AWS_SECRET_ACCESS_KEY="wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"
export AWS_DEFAULT_REGION="us-east-1"
```

> Variáveis de ambiente têm precedência sobre os arquivos `~/.aws/credentials` e `~/.aws/config`.

---

## Referências oficiais

- [Instalação do AWS CLI v2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- [Configuração do AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)
- [Gerenciamento de Access Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)
- [AWS STS – get-caller-identity](https://docs.aws.amazon.com/cli/latest/reference/sts/get-caller-identity.html)
- [Boas práticas de segurança IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Múltiplos perfis no AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
