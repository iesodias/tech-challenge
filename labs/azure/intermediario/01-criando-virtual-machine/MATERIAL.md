# Material de Estudo — Virtual Machine (Azure)

> Resumo de apoio para o [Lab 01](README.md) | [Quiz](../../../../.github/ISSUE_TEMPLATE/quiz-azure-intermediario-01-criando-virtual-machine.yml)

---

## O que é uma Virtual Machine?

Uma **Virtual Machine (VM)** é um computador virtualizado no Azure que permite executar sistemas operacionais e aplicações na nuvem. Ela fornece recursos de computação sob demanda (CPU, memória, disco e rede) sem a necessidade de manter hardware físico. VMs são ideais para hospedar aplicações, testar ambientes e executar cargas de trabalho diversas.

---

## Conceitos-chave

- **Resource Group:** Contêiner lógico que agrupa recursos relacionados. Ao criar um grupo dedicado para a VM, todos os recursos associados podem ser excluídos de uma só vez.
- **Image (Imagem):** Define o sistema operacional e software pré-instalado da VM. Exemplo: Ubuntu Server 24.04 LTS.
- **Size (Tamanho):** Determina a quantidade de vCPUs, memória RAM e capacidade de disco da VM. O **Standard_B1s** é econômico e adequado para testes.
- **Virtual Network (VNet):** Rede privada isolada onde a VM é conectada. O Azure cria automaticamente uma VNet, sub-rede e IP público durante a criação da VM.
- **Network Security Group (NSG):** Funciona como um firewall virtual, controlando o tráfego de entrada e saída da VM com base em regras de porta e protocolo.
- **Public IP:** Endereço IP público que permite acessar a VM pela internet (ex: via SSH na porta 22).
- **OS Disk:** Disco que armazena o sistema operacional. O tipo **Standard SSD** oferece bom equilíbrio entre custo e desempenho.
- **Trusted Launch:** Tipo de segurança que protege a VM com Secure Boot e vTPM contra ameaças de boot.
- **Tags:** Pares chave-valor para organizar, categorizar e filtrar recursos no Azure.

---

## Resumo de configurações do lab

| Configuração | Valor |
|---|---|
| Resource Group | `lab-vm-rg` |
| Nome da VM | `lab-vm-01` |
| Região | Brazil South |
| Imagem | Ubuntu Server 24.04 LTS - x64 Gen2 |
| Tamanho | Standard_B1s (1 vCPU, 1 GiB RAM) |
| Autenticação | Password |
| Usuário | `azureuser` |
| Porta de entrada | SSH (22) |
| Tipo de disco | Standard SSD (30 GiB) |
| Redundância do disco | LRS (Locally-redundant) |

---

## Boas práticas

- **Use SSH keys em produção:** Autenticação por chave SSH é mais segura que senha. Passwords são aceitáveis apenas para labs.
- **Marque "Delete with VM":** Garanta que disco, NIC e IP público sejam excluídos junto com a VM para evitar custos com recursos órfãos.
- **Restrinja portas de entrada:** Em produção, limite o acesso SSH por IP de origem em vez de permitir acesso de qualquer endereço.
- **Exclua o Resource Group inteiro:** É a forma mais segura de limpar todos os recursos de um lab, removendo VM, disco, NIC, IP, VNet e NSG de uma vez.

---

📝 [Responda o quiz para testar seu conhecimento](../../../../.github/ISSUE_TEMPLATE/quiz-azure-intermediario-01-criando-virtual-machine.yml)
