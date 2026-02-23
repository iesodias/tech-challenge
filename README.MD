# Tech Challenge — Labs Práticos de Cloud

Repositório com desafios técnicos curtos e práticos de **AWS** e **Azure** para quem está começando na área de TI e quer aprender cloud na prática.

---

## Objetivo

Ajudar pessoas que querem entrar na área de tecnologia a dar os primeiros passos com cloud computing. Aqui você vai encontrar labs passo a passo, do básico ao intermediário, usando apenas a linha de comando (CLI).

Nada de teoria longa — é tudo mão na massa. Cada lab é curto, direto e focado em **um único recurso** da nuvem.

---

## Como funciona

Cada lab segue um formato padronizado:

- **5 a 10 passos** no máximo
- **Um comando por passo** com explicação das flags
- **Pré-requisitos** claros (CLI instalada, conta ativa)
- **Limpeza** no final para não gerar custos

---

## Estrutura

```
labs/
├── aws/
│   ├── basico/
│   │   ├── 01-criando-s3-bucket/README.md
│   │   └── 02-configurando-iam-user/README.md
│   └── intermediario/
│       └── 01-criando-vpc/README.md
└── azure/
    ├── basico/
    │   ├── 01-criando-resource-group/README.md
    │   └── 02-criando-storage-account/README.md
    └── intermediario/
        └── 01-criando-virtual-machine/README.md
```

Organizado por cloud (`aws`/`azure`) e nivel de dificuldade (`basico`/`intermediario`). Cada lab tem sua propria pasta com um `README.md` contendo o passo a passo completo.

---

## Clouds Suportadas

| Provedor | CLI |
|----------|-----|
| AWS      | `aws cli` |
| Azure    | `az cli`  |

---

## Como começar

### 1. Crie sua conta gratuita na cloud

Antes de tudo, voce precisa de uma conta gratuita. Escolha AWS, Azure ou ambas:

#### Conta Gratuita AWS

A AWS oferece o **Free Plan** com ate $200 USD em creditos e 6 meses de uso gratuito de servicos selecionados.

**Requisitos:**
- E-mail valido
- Cartao de credito ou debito internacional (para verificacao, sem cobranca no plano gratuito)
- Numero de telefone para verificacao por SMS ou chamada
- Documento de identidade

**Passo a passo:**
1. Acesse [https://aws.amazon.com/free](https://aws.amazon.com/free/)
2. Clique em **Create an AWS Account**
3. Informe seu e-mail e crie uma senha para o root user
4. Preencha as informacoes da conta (pessoal ou empresarial)
5. Adicione um metodo de pagamento valido
6. Complete a verificacao de identidade por telefone (SMS ou chamada)
7. Escolha o plano de suporte **Basic (Free)**
8. Aguarde a ativacao (geralmente leva minutos, pode levar ate 24h)
9. Voce recebera um e-mail de confirmacao quando a conta estiver ativa

> **Dica:** Use um e-mail que voce nao vai perder acesso. Ative MFA (autenticacao multifator) na conta root assim que possivel.

**Links uteis:**
- [Pagina do Free Tier](https://aws.amazon.com/free/)
- [Guia de criacao de conta](https://repost.aws/knowledge-center/create-and-activate-aws-account)
- [Console AWS](https://console.aws.amazon.com/)

---

#### Conta Gratuita Azure

A Azure oferece **65+ servicos sempre gratuitos**, alem de servicos gratuitos por 12 meses para novos clientes.

**Requisitos:**
- Conta Microsoft (Outlook, Hotmail ou qualquer e-mail)
- Cartao de credito ou debito internacional (para verificacao)
- Numero de telefone para verificacao
- Documento de identidade

**Passo a passo:**
1. Acesse [https://azure.microsoft.com/free](https://azure.microsoft.com/en-us/pricing/free-services)
2. Clique em **Start free** ou **Get started with Azure**
3. Faca login com sua conta Microsoft (ou crie uma)
4. Preencha seus dados pessoais e endereco
5. Complete a verificacao de identidade por telefone
6. Adicione um cartao de credito/debito para verificacao
7. Aceite os termos e condicoes
8. Pronto! Voce tera acesso ao portal [https://portal.azure.com](https://portal.azure.com)

> **Dica:** Estudantes podem usar o [Azure for Students](https://azure.microsoft.com/en-us/free/students/) com $100 USD em creditos sem precisar de cartao de credito — basta um e-mail academico.

**Links uteis:**
- [Servicos gratuitos do Azure](https://azure.microsoft.com/en-us/pricing/free-services)
- [Portal Azure](https://portal.azure.com)
- [Azure for Students](https://azure.microsoft.com/en-us/free/students/)
- [Calculadora de precos](https://azure.microsoft.com/en-us/pricing/calculator/)

---

## Labs Disponíveis

### Azure — Básico

| #  | Lab | Descrição |
|----|-----|-----------|
| 01 | [Criar um Resource Group pelo Portal Azure](labs/azure/basico/01-criando-resource-group/README.md) | Crie seu primeiro grupo de recursos usando o Portal Azure |
| 02 | [Criar uma Storage Account pelo Portal Azure](labs/azure/basico/02-criando-storage-account/README.md) | Crie sua primeira conta de armazenamento usando o Portal Azure |

---

## Contribuindo

Quer sugerir um novo lab ou corrigir algo? Abra uma [issue](../../issues) ou envie um pull request.

---

## Licença

Este projeto é open source e está disponível sob a licença [MIT](LICENSE).