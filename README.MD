<div align="center">

# ☁️ Tech Challenge — Labs Práticos de Cloud

![Labs](https://img.shields.io/badge/Labs-2-blue?style=for-the-badge)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow?style=for-the-badge)
![Licença](https://img.shields.io/badge/Licen%C3%A7a-MIT-green?style=for-the-badge)
![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge)

**Aprenda cloud na prática com labs curtos, diretos e mão na massa.**

[Começar Agora](#-como-começar) · [Ver Labs](#-labs-disponíveis) · [Contribuir](#-contribuindo)

</div>

---

## 🎯 Objetivo

Ajudar pessoas que querem entrar na área de tecnologia a dar os primeiros passos com cloud computing. Aqui você vai encontrar labs passo a passo, do básico ao intermediário.

> **Nada de teoria longa — é tudo mão na massa.** Cada lab é curto, direto e focado em **um único recurso** da nuvem.

---

## ⚙️ Como funciona

Cada lab segue um formato padronizado:

| | Regra |
|---|---|
| 📝 | **5 a 10 passos** no máximo |
| 🎯 | **Uma ação por passo** com explicação detalhada |
| ✅ | **Pré-requisitos** claros no início |
| 🧹 | **Limpeza** no final para não gerar custos |

---

## 📁 Estrutura

```
labs/
├── aws/
│   ├── basico/
│   └── intermediario/
└── azure/
    ├── basico/
    │   ├── 01-criando-resource-group/
    │   └── 02-criando-storage-account/
    └── intermediario/
```

Organizado por cloud (`aws`/`azure`) e nível de dificuldade (`basico`/`intermediario`). Cada lab tem sua própria pasta com um `README.md` contendo o passo a passo completo.

---

## ☁️ Clouds Suportadas

| Provedor | Ferramenta | Status |
|----------|------------|--------|
| ![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white) | Portal / `az cli` | ✅ Ativo |
| ![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white) | Console / `aws cli` | 🔜 Em breve |

---

## 🚀 Como começar

### 1. Crie sua conta gratuita na cloud

Antes de tudo, você precisa de uma conta gratuita. Escolha AWS, Azure ou ambas:

<details>
<summary><strong>☁️ Conta Gratuita AWS</strong></summary>

<br>

A AWS oferece o **Free Plan** com até $200 USD em créditos e 6 meses de uso gratuito de serviços selecionados.

**Requisitos:**
- E-mail válido
- Cartão de crédito ou débito internacional (para verificação, sem cobrança no plano gratuito)
- Número de telefone para verificação por SMS ou chamada
- Documento de identidade

**Passo a passo:**
1. Acesse [https://aws.amazon.com/free](https://aws.amazon.com/free/)
2. Clique em **Create an AWS Account**
3. Informe seu e-mail e crie uma senha para o root user
4. Preencha as informações da conta (pessoal ou empresarial)
5. Adicione um método de pagamento válido
6. Complete a verificação de identidade por telefone (SMS ou chamada)
7. Escolha o plano de suporte **Basic (Free)**
8. Aguarde a ativação (geralmente leva minutos, pode levar até 24h)
9. Você receberá um e-mail de confirmação quando a conta estiver ativa

> **💡 Dica:** Use um e-mail que você não vai perder acesso. Ative MFA (autenticação multifator) na conta root assim que possível.

**Links úteis:**
- [Página do Free Tier](https://aws.amazon.com/free/)
- [Guia de criação de conta](https://repost.aws/knowledge-center/create-and-activate-aws-account)
- [Console AWS](https://console.aws.amazon.com/)

</details>

<details>
<summary><strong>🔷 Conta Gratuita Azure</strong></summary>

<br>

A Azure oferece **65+ serviços sempre gratuitos**, além de serviços gratuitos por 12 meses para novos clientes.

**Requisitos:**
- Conta Microsoft (Outlook, Hotmail ou qualquer e-mail)
- Cartão de crédito ou débito internacional (para verificação)
- Número de telefone para verificação
- Documento de identidade

**Passo a passo:**
1. Acesse [https://azure.microsoft.com/free](https://azure.microsoft.com/en-us/pricing/free-services)
2. Clique em **Start free** ou **Get started with Azure**
3. Faça login com sua conta Microsoft (ou crie uma)
4. Preencha seus dados pessoais e endereço
5. Complete a verificação de identidade por telefone
6. Adicione um cartão de crédito/débito para verificação
7. Aceite os termos e condições
8. Pronto! Você terá acesso ao portal [https://portal.azure.com](https://portal.azure.com)

> **💡 Dica:** Estudantes podem usar o [Azure for Students](https://azure.microsoft.com/en-us/free/students/) com $100 USD em créditos sem precisar de cartão de crédito — basta um e-mail acadêmico.

**Links úteis:**
- [Serviços gratuitos do Azure](https://azure.microsoft.com/en-us/pricing/free-services)
- [Portal Azure](https://portal.azure.com)
- [Azure for Students](https://azure.microsoft.com/en-us/free/students/)
- [Calculadora de preços](https://azure.microsoft.com/en-us/pricing/calculator/)

</details>

---

## 📚 Labs Disponíveis

### 🔷 Azure — Básico

| # | Lab | Nível | Ferramenta |
|---|-----|-------|------------|
| 01 | [Criar um Resource Group pelo Portal Azure](labs/azure/basico/01-criando-resource-group/README.md) | ![Básico](https://img.shields.io/badge/Básico-4CAF50?style=flat-square) | ![Portal](https://img.shields.io/badge/Portal-0078D4?style=flat-square&logo=microsoftazure&logoColor=white) |
| 02 | [Criar uma Storage Account pelo Portal Azure](labs/azure/basico/02-criando-storage-account/README.md) | ![Básico](https://img.shields.io/badge/Básico-4CAF50?style=flat-square) | ![Portal](https://img.shields.io/badge/Portal-0078D4?style=flat-square&logo=microsoftazure&logoColor=white) |

### ☁️ AWS — Básico

| # | Lab | Nível | Ferramenta |
|---|-----|-------|------------|
| — | *Em breve* | — | — |

---

## 🤝 Contribuindo

Quer sugerir um novo lab ou corrigir algo?

1. Faça um fork do projeto
2. Crie uma branch (`git checkout -b feature/novo-lab`)
3. Faça suas alterações e commit (`git commit -m 'feat: adiciona novo lab'`)
4. Push para a branch (`git push origin feature/novo-lab`)
5. Abra um [Pull Request](../../pulls)

Ou simplesmente abra uma [issue](../../issues) com sua sugestão.

---

## 📄 Licença

Este projeto é open source e está disponível sob a licença [MIT](LICENSE).

---

<div align="center">

Feito com ❤️ para a comunidade de cloud

</div>