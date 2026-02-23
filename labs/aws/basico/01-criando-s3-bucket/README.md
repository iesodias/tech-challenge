# Lab AWS – Criar um Bucket S3 pelo Console AWS

Neste lab você vai aprender a criar seu primeiro **Bucket S3** (Simple Storage Service) usando o Console AWS. O S3 é o serviço de armazenamento de objetos da AWS — ele permite guardar e recuperar qualquer quantidade de dados de qualquer lugar da web.

---

## Pré-requisitos

- Conta ativa na AWS (pode ser a [conta gratuita AWS Free Tier](https://aws.amazon.com/pt/free/))
- Navegador web atualizado (Chrome, Edge, Firefox)
- Acesso ao [Console AWS](https://console.aws.amazon.com)
- Um arquivo de texto simples no seu computador para upload (ex: `meu-arquivo.txt`)

---

## 1. Fazer login no Console AWS

Abra o navegador e acesse **[https://console.aws.amazon.com](https://console.aws.amazon.com)**. Insira seu e-mail (ou ID da conta), senha e conclua a autenticação. Após o login, você será direcionado à página inicial do Console AWS.

> **Console AWS (AWS Management Console)** é a interface web de gerenciamento da AWS. Por ele você pode criar, configurar, monitorar e excluir todos os recursos da sua conta. A página inicial mostra uma barra de pesquisa no topo, atalhos para serviços recentes e widgets personalizáveis.

---

## 2. Navegar até o serviço Amazon S3

Na página inicial do console, localize a **barra de pesquisa** no topo da tela. Digite **"S3"** e clique na opção **"S3"** que aparece nos resultados sob a seção **Serviços**. Você será levado ao painel do Amazon S3.

> **Amazon S3 (Simple Storage Service)** é o serviço de armazenamento de objetos da AWS. Ele permite armazenar arquivos (chamados de "objetos") dentro de contêineres chamados "buckets". Cada objeto pode ter até 5 TB e é acessado via uma URL única. O S3 é usado para backups, hospedagem de sites estáticos, armazenamento de mídia, data lakes e muito mais.

---

## 3. Iniciar a criação de um novo bucket

No painel do Amazon S3, clique em **"General purpose buckets"** (Buckets de uso geral) no menu de navegação à esquerda. Em seguida, clique no botão **"Create bucket"** (Criar bucket) no canto superior direito da página. Isso abrirá o formulário de criação de um novo bucket.

> **Bucket** é o contêiner principal do S3 onde você armazena seus objetos (arquivos). Todo objeto no S3 precisa estar dentro de um bucket. O nome do bucket precisa ser **globalmente único** em toda a AWS — nenhuma outra conta no mundo pode ter um bucket com o mesmo nome. O tipo **"General purpose"** (uso geral) é o padrão para a maioria dos casos de uso.

---

## 4. Preencher as configurações do bucket

Na página **"Create bucket"**, preencha e revise os seguintes campos:

- **Bucket type (Tipo de bucket):** Mantenha selecionado **"General purpose"**
- **Bucket name (Nome do bucket):** Digite um nome único, por exemplo: **`meu-primeiro-bucket-lab-XXXX`** (substitua `XXXX` por números aleatórios para garantir unicidade, ex: `meu-primeiro-bucket-lab-2026`)
- **AWS Region (Região):** Selecione **`South America (São Paulo) sa-east-1`**
- **Object Ownership (Propriedade de objetos):** Mantenha a opção padrão **"ACLs disabled (recommended)"** — ACLs desabilitadas
- **Block Public Access settings for this bucket:** Mantenha **todas as opções marcadas** (Block *all* public access habilitado) — este é o padrão
- **Bucket Versioning (Versionamento):** Mantenha **"Disable"** (Desabilitado)
- **Default encryption (Criptografia padrão):** Mantenha **"Server-side encryption with Amazon S3 managed keys (SSE-S3)"**

Após revisar todas as configurações, clique no botão **"Create bucket"** (Criar bucket) na parte inferior da página.

> - **Bucket name:** Deve ser globalmente único, ter entre 3 e 63 caracteres, usar apenas letras minúsculas, números e hífens. Não pode começar ou terminar com hífen.
> - **AWS Region:** Define a região geográfica onde seus dados serão armazenados fisicamente. Escolhemos **sa-east-1 (São Paulo)** para menor latência no Brasil.
> - **ACLs disabled (recommended):** Com ACLs desabilitadas, o proprietário do bucket tem controle total sobre todos os objetos. Esta é a configuração recomendada pela AWS.
> - **Block all public access:** Bloqueia qualquer acesso público ao bucket e seus objetos. Sempre mantenha habilitado a menos que você tenha um caso de uso específico (como hospedagem de site estático).
> - **Bucket Versioning:** Quando habilitado, mantém múltiplas versões de um mesmo objeto. Para este lab, não é necessário.
> - **SSE-S3:** É a criptografia padrão do S3 gerenciada automaticamente pela AWS. Todos os objetos são criptografados em repouso sem custo adicional.

---

## 5. Verificar o bucket criado

Após a criação, você será redirecionado para a lista de buckets. Para confirmar:

1. Na lista de **"General purpose buckets"**, localize o bucket que você acabou de criar (ex: `meu-primeiro-bucket-lab-2026`)
2. Clique no nome do bucket para abrir a página de detalhes
3. Observe as abas disponíveis: **Objects**, **Properties**, **Permissions**, **Metrics**, **Management** e **Access Points**

Na aba **Properties**, você pode conferir a região, o versionamento, a criptografia e outras configurações do bucket.

> Após criar qualquer recurso na AWS, é uma boa prática verificar se ele foi provisionado corretamente. A página de detalhes do bucket mostra todas as configurações e permite gerenciar objetos, permissões e propriedades. A aba **Objects** é onde você verá os arquivos armazenados.

---

## 6. Fazer upload de um arquivo para o bucket

Na página do seu bucket, certifique-se de estar na aba **"Objects"** (Objetos). Em seguida:

1. Clique no botão **"Upload"**
2. Na página de upload, na seção **"Files and folders"**, clique em **"Add files"** (Adicionar arquivos)
3. Selecione o arquivo de texto do seu computador (ex: `meu-arquivo.txt`) e clique em **"Open"** (Abrir)
4. O arquivo aparecerá listado na seção de upload. Revise e clique no botão **"Upload"** na parte inferior da página
5. Aguarde a mensagem de sucesso **"Upload succeeded"** e clique em **"Close"** (Fechar)

> Quando você faz upload de um arquivo para o S3, ele se torna um **objeto**. Cada objeto é composto por: o arquivo em si (dados), um identificador único chamado **key** (chave — que é o nome do arquivo/caminho), e metadados (tipo de conteúdo, data de criação, etc.). O S3 suporta upload de arquivos de até **5 TB** por objeto.

---

## 7. Fazer download do objeto

De volta à aba **"Objects"** do seu bucket, você verá o arquivo que acabou de enviar listado. Para fazer o download:

1. Marque o **checkbox** (caixa de seleção) ao lado do nome do arquivo
2. Clique no botão **"Download"** que aparece no topo da lista de objetos
3. O arquivo será baixado para a pasta de downloads padrão do seu navegador

> O download pelo console é a forma mais simples de recuperar um objeto do S3. Para acesso programático, você pode usar a AWS CLI, SDKs ou URLs pré-assinadas (presigned URLs). Cada objeto no S3 possui uma **URL única**, mas por padrão ela não é acessível publicamente devido ao Block Public Access que configuramos.

---

## 8. Limpeza dos recursos

Para evitar qualquer custo e manter sua conta organizada, vamos excluir o objeto e o bucket criados:

**Passo A — Excluir o objeto:**

1. Na aba **"Objects"** do bucket, marque o **checkbox** ao lado do arquivo enviado
2. Clique no botão **"Delete"** (Excluir)
3. Na página de confirmação, digite **`permanently delete`** no campo de texto
4. Clique no botão **"Delete objects"** (Excluir objetos)

**Passo B — Excluir o bucket:**

1. Clique em **"General purpose buckets"** no menu de navegação à esquerda para voltar à lista de buckets
2. Selecione o **botão de opção** (radio button) ao lado do nome do bucket `meu-primeiro-bucket-lab-2026`
3. Clique no botão **"Delete"** (Excluir) no topo da página
4. Na página de confirmação, digite o **nome do bucket** no campo de texto
5. Clique no botão **"Delete bucket"** (Excluir bucket)

> O S3 só permite excluir um bucket que esteja **completamente vazio** — por isso excluímos o objeto primeiro. A AWS exige que você digite `permanently delete` (para objetos) e o nome do bucket (para o bucket) como confirmação para evitar exclusões acidentais. O Bucket S3 do Free Tier oferece **5 GB de armazenamento gratuito**, mas é sempre boa prática limpar recursos de lab para evitar surpresas na fatura.

---

## 🎉 Finalizou o lab? Compartilhe!

Use o template abaixo para postar no LinkedIn — basta copiar, ajustar o que quiser e publicar!

```
☁️ Mais um lab concluído!

Hoje aprendi a criar um Bucket S3 e fazer upload de arquivos usando o Console AWS.

✅ O que pratiquei:
• Criar um Bucket S3 com nome globalmente único na região sa-east-1
• Fazer upload e download de objetos diretamente pelo Console AWS
• Manter o Block Public Access habilitado e limpar os recursos ao final

📖 Lab completo e gratuito:
https://github.com/iesodias/tech-challenge/blob/main/labs/aws/basico/01-criando-s3-bucket/README.md

🗂️ Repositório com todos os labs:
https://github.com/iesodias/tech-challenge

#AWS #Cloud #CloudComputing #TechChallenge #AprendizadoContínuo #DevOps
```
