# Material de Estudo — Resource Group

> Resumo de apoio para o [Lab 01](README.md) | [Quiz](../../../../.github/ISSUE_TEMPLATE/quiz-azure-basico-01-criando-resource-group.yml)

---

## O que é Resource Group?

**Resource Group** (Grupo de Recursos) é um contêiner lógico que agrupa recursos relacionados no Azure. Todo recurso — VMs, bancos de dados, contas de armazenamento — precisa pertencer a um Resource Group. Ele permite gerenciar, controlar acesso e excluir recursos como uma unidade.

---

## Conceitos-chave

- **Contêiner lógico:** Não é um recurso em si, mas uma forma de organizar recursos relacionados (por projeto, ambiente ou ciclo de vida)
- **Subscription (Assinatura):** Contrato de cobrança do Azure ao qual o Resource Group e seus recursos estão vinculados
- **Region (Região):** Define onde os **metadados** do Resource Group são armazenados — os recursos dentro dele podem estar em regiões diferentes
- **Tags:** Pares de chave-valor para organizar recursos logicamente, facilitar a gestão de custos e automatizar políticas
- **Review + create:** Etapa de validação automática do Azure antes de provisionar o recurso
- **Exclusão em cascata:** Ao excluir um Resource Group, todos os recursos dentro dele são excluídos automaticamente

---

## Resumo de configurações do lab

| Configuração | Valor usado no lab |
|---|---|
| Nome do Resource Group | `lab-rg-01` |
| Região | Brazil South (São Paulo) |
| Tag 1 | `Ambiente: Lab` |
| Tag 2 | `Projeto: TechChallenge` |

---

## Boas práticas

- **Use Resource Groups para ambientes temporários** — basta excluir o grupo para limpar tudo de uma vez
- **Aplique tags desde o início** — facilita filtrar custos e identificar recursos em assinaturas com muitos serviços
- **Escolha a região mais próxima** dos seus usuários para reduzir latência
- **Sempre execute a limpeza** ao final de labs para evitar custos desnecessários e manter a assinatura organizada

---

📝 [Responda o quiz para testar seu conhecimento](../../../../.github/ISSUE_TEMPLATE/quiz-azure-basico-01-criando-resource-group.yml)
