# Lab {{CLOUD_PROVIDER}} – {{VERB}} {{RESOURCE}} com {{TOOL}}

{{SHORT_INTRO}}

---

## Pré-requisitos

- {{PREREQUISITE_1}}
- {{PREREQUISITE_2}}
- {{PREREQUISITE_3}}

---

## 1. {{STEP_1_TITLE}}

```bash
{{STEP_1_COMMAND}}
```

> {{STEP_1_EXPLANATION}}

---

## 2. {{STEP_2_TITLE}}

```bash
{{STEP_2_COMMAND}}
```

> {{STEP_2_EXPLANATION}}

---

## 3. {{STEP_3_TITLE}}

```bash
{{STEP_3_COMMAND}}
```

> {{STEP_3_EXPLANATION}}

---

## 4. {{STEP_4_TITLE}}

```bash
{{STEP_4_COMMAND}}
```

> {{STEP_4_EXPLANATION}}

---

## 5. {{STEP_5_TITLE}}

```bash
{{STEP_5_COMMAND}}
```

> {{STEP_5_EXPLANATION}}

---

{{OPTIONAL_EXTRA_STEPS}}

## {{CLEANUP_STEP_NUMBER}}. Limpeza dos recursos

```bash
{{CLEANUP_COMMAND}}
```

> {{CLEANUP_EXPLANATION}}

---

<!--
INSTRUÇÕES PARA O AGENTE:

Placeholders obrigatórios:
- {{CLOUD_PROVIDER}}: "AWS" ou "Azure"
- {{VERB}}: Verbo no infinitivo (ex: Criar, Configurar, Provisionar, Implantar)
- {{RESOURCE}}: Recurso da nuvem (ex: Instância EC2, Storage Account, S3 Bucket, Resource Group)
- {{TOOL}}: Ferramenta CLI utilizada (ex: AWS CLI, Azure CLI, Terraform, Pulumi)
- {{SHORT_INTRO}}: 1-2 frases curtas descrevendo o que o lab ensina
- {{PREREQUISITE_N}}: Itens necessários (ex: Conta AWS ativa, AWS CLI instalado e configurado)
- {{STEP_N_TITLE}}: Nome curto da ação (ex: Criar o Security Group, Configurar a VPC)
- {{STEP_N_COMMAND}}: Comando bash único para a ação
- {{STEP_N_EXPLANATION}}: Explicação das flags e parâmetros do comando
- {{CLEANUP_STEP_NUMBER}}: Número do último passo (limpeza)
- {{CLEANUP_COMMAND}}: Comando(s) para destruir todos os recursos criados
- {{CLEANUP_EXPLANATION}}: Explicação do comando de limpeza
- {{OPTIONAL_EXTRA_STEPS}}: Passos adicionais (6-10) se necessário, seguindo o mesmo formato. Deixar vazio se não precisar.

Regras:
1. O lab deve ter entre 5 e 10 passos no total (incluindo limpeza)
2. Cada passo deve conter UMA ÚNICA ação
3. Todo bloco de código deve ser seguido de um blockquote (>) explicando flags/parâmetros
4. Usar separadores (---) entre cada seção
5. O último passo SEMPRE deve ser a limpeza dos recursos criados
6. Idioma: Português (pt-BR)
7. Manter o lab curto e prático para iniciantes
-->
