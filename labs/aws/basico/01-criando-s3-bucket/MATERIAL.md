# Material de Estudo — Amazon S3 Bucket

> Resumo de apoio para o [Lab 01](README.md) | [Quiz](../../../../.github/ISSUE_TEMPLATE/quiz-aws-basico-01-criando-s3-bucket.yml)

---

## O que é Amazon S3?

**Amazon S3** (Simple Storage Service) é o serviço de armazenamento de objetos da AWS. Ele permite armazenar e recuperar qualquer quantidade de dados de qualquer lugar da web. Os dados são organizados em **buckets** (contêineres) e **objetos** (arquivos + metadados).

---

## Conceitos-chave

- **Bucket:** Contêiner principal onde objetos são armazenados. O nome deve ser **globalmente único** em toda a AWS, pois faz parte da URL de acesso
- **Objeto:** Um arquivo armazenado no S3, composto por dados, uma **key** (chave/nome) e metadados como tipo de conteúdo e data de criação
- **Region (Região):** Define onde os dados do bucket são armazenados fisicamente — escolha a região mais próxima para menor latência
- **Block Public Access:** Configuração que impede acesso público aos objetos do bucket — deve ser mantida habilitada por padrão
- **ACLs disabled (recommended):** Com ACLs desabilitadas, o proprietário do bucket tem controle total sobre todos os objetos, simplificando o gerenciamento de permissões
- **SSE-S3:** Criptografia padrão gerenciada pela AWS que protege os dados em repouso automaticamente e sem custo adicional
- **Bucket Versioning:** Quando habilitado, mantém múltiplas versões de um mesmo objeto, permitindo recuperar versões anteriores

---

## Resumo de configurações do lab

| Configuração | Valor usado no lab |
|---|---|
| Tipo de bucket | General purpose |
| Região | sa-east-1 (São Paulo) |
| Object Ownership | ACLs disabled (recommended) |
| Block Public Access | Habilitado (todas as opções) |
| Bucket Versioning | Desabilitado |
| Criptografia padrão | SSE-S3 |

---

## Boas práticas

- **Mantenha o Block Public Access habilitado** — só desabilite se tiver um caso de uso específico como hospedagem de site estático
- **Use nomes descritivos e padronizados** para buckets, incluindo ambiente e projeto (ex: `projeto-ambiente-funcao`)
- **Sempre esvazie o bucket antes de excluí-lo** — o S3 só permite deletar buckets completamente vazios
- **Limpe recursos de lab ao final** — o Free Tier oferece 5 GB gratuitos, mas é boa prática evitar acúmulo de recursos desnecessários

---

📝 [Responda o quiz para testar seu conhecimento](../../../../.github/ISSUE_TEMPLATE/quiz-aws-basico-01-criando-s3-bucket.yml)
