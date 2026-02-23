# Lab Azure – Criar uma Virtual Machine pelo Portal Azure

Neste lab você vai aprender a criar sua primeira **Virtual Machine (Máquina Virtual)** usando o Portal Azure, passando por todas as abas de configuração com apenas as informações básicas necessárias. A VM é um dos recursos mais utilizados no Azure para executar aplicações, testar ambientes e hospedar serviços.

---

## Pré-requisitos

- Conta ativa no Microsoft Azure (pode ser a [conta gratuita](https://azure.microsoft.com/pt-br/free/))
- Navegador web atualizado (Chrome, Edge, Firefox)
- Acesso ao [Portal Azure](https://portal.azure.com)

---

## 1. Fazer login no Portal Azure

Abra o navegador e acesse **[https://portal.azure.com](https://portal.azure.com)**. Insira seu e-mail e senha da conta Microsoft associada à sua assinatura Azure. Após autenticar, você será direcionado à página inicial do portal.

> **Portal Azure** é a interface web de gerenciamento do Azure. Por ele você pode criar, configurar, monitorar e excluir todos os recursos da sua conta. A página inicial mostra um painel (dashboard) com atalhos e recursos recentes.

---

## 2. Criar um Resource Group para o lab

Antes de criar a VM, vamos criar um Resource Group dedicado para agrupar todos os recursos do lab (VM, disco, rede, IP público, etc.). Isso facilita a limpeza no final.

1. Na barra de pesquisa do portal, digite **"Resource groups"** e clique no resultado
2. Clique no botão **"+ Create"** (ou **"+ Criar"**)
3. Preencha os campos:
   - **Subscription (Assinatura):** Selecione a sua assinatura Azure
   - **Resource group:** Digite **`lab-vm-rg`**
   - **Region:** Selecione **`(South America) Brazil South`**
4. Clique em **"Review + create"** e depois em **"Create"**

> **Resource Group** é um contêiner lógico que agrupa recursos relacionados no Azure. Criamos um grupo dedicado (`lab-vm-rg`) para que, ao final do lab, possamos excluir o grupo inteiro e todos os recursos associados à VM (disco, placa de rede, IP público, rede virtual, grupo de segurança) sejam removidos automaticamente.

---

## 3. Navegar até Virtual Machines e iniciar a criação

Na barra de pesquisa do portal, digite **"Virtual machines"** e clique na opção **"Virtual machines"** nos resultados sob **Serviços**. Na página de Virtual Machines, clique no botão **"+ Create"** e selecione **"Azure virtual machine"** no menu suspenso.

> A página de **Virtual Machines** lista todas as VMs da sua assinatura. O botão **"+ Create"** oferece opções como "Azure virtual machine" (criação completa com todas as abas de configuração), "Azure virtual machine with preset configuration" (configuração predefinida) e outras. Escolhemos a opção padrão para passar por todas as abas de configuração.

---

## 4. Preencher a aba Basics (Básico)

Na aba **"Basics"**, preencha os seguintes campos:

**Detalhes do projeto:**
- **Subscription (Assinatura):** Selecione a sua assinatura Azure
- **Resource group:** Selecione **`lab-vm-rg`** (criado no passo anterior)

**Detalhes da instância:**
- **Virtual machine name (Nome):** Digite **`lab-vm-01`**
- **Region (Região):** Selecione **`(South America) Brazil South`**
- **Availability options (Opções de disponibilidade):** Mantenha **`No infrastructure redundancy required`**
- **Security type (Tipo de segurança):** Mantenha **`Trusted launch virtual machines`**
- **Image (Imagem):** Selecione **`Ubuntu Server 24.04 LTS - x64 Gen2`**
- **VM architecture:** Mantenha **`x64`**
- **Size (Tamanho):** Clique em **"See all sizes"** e selecione **`Standard_B1s`** (1 vCPU, 1 GiB RAM)

**Conta de administrador:**
- **Authentication type (Tipo de autenticação):** Selecione **`Password`**
- **Username (Nome de usuário):** Digite **`azureuser`**
- **Password (Senha):** Digite uma senha forte (mínimo 12 caracteres, com maiúsculas, minúsculas, números e caracteres especiais)
- **Confirm password:** Repita a mesma senha

**Regras de porta de entrada:**
- **Public inbound ports (Portas de entrada públicas):** Selecione **`Allow selected ports`**
- **Select inbound ports (Selecionar portas):** Marque **`SSH (22)`**

> - **Resource group:** Associamos a VM ao `lab-vm-rg` para facilitar a limpeza posterior.
> - **Virtual machine name:** O nome identifica a VM no Azure e também será o hostname do sistema operacional.
> - **Region:** Define o data center onde a VM será fisicamente hospedada. **Brazil South** é a região mais próxima do Brasil.
> - **Availability options:** `No infrastructure redundancy required` significa que a VM não terá redundância de infraestrutura — suficiente para um lab.
> - **Security type:** `Trusted launch` fornece segurança aprimorada com Secure Boot e vTPM, protegendo contra ameaças de boot.
> - **Image:** A imagem define o sistema operacional. **Ubuntu Server 24.04 LTS** é uma distribuição Linux estável e amplamente usada.
> - **Size:** `Standard_B1s` é um dos tamanhos mais baratos, ideal para labs e testes leves (1 vCPU, 1 GiB RAM). Clique em "See all sizes" para ver todas as opções disponíveis.
> - **Authentication type:** `Password` é a opção mais simples para labs. Para ambientes de produção, é recomendado usar **SSH public key** por ser mais seguro.
> - **Public inbound ports:** Permitir a porta **SSH (22)** possibilita a conexão remota à VM via terminal. Em produção, restrinja o acesso por IP de origem.

---

## 5. Configurar a aba Disks (Discos)

Clique em **"Next: Disks >"** para avançar. Na aba **"Disks"**, configure:

- **OS disk size (Tamanho do disco do SO):** Mantenha **`Default size (30 GiB)`**
- **OS disk type (Tipo de disco do SO):** Selecione **`Standard SSD (locally-redundant storage)`**
- **Delete with VM (Excluir com a VM):** Mantenha **marcado** ✔️

Não adicione discos de dados extras. Mantenha os demais campos com os valores padrão.

> - **OS disk type:** Define a performance e custo do disco do sistema operacional. **Standard SSD** oferece um bom equilíbrio entre custo e desempenho para labs, sendo mais rápido que o HDD padrão e mais barato que o Premium SSD.
> - **OS disk size:** O tamanho padrão de 30 GiB é suficiente para o sistema operacional Ubuntu e testes básicos.
> - **Delete with VM:** Quando marcado, o disco é excluído automaticamente ao deletar a VM, evitando custos de discos órfãos. Fundamental para labs.
> - **Discos de dados:** São discos adicionais para armazenamento de aplicações e dados. Não são necessários para este lab.

---

## 6. Configurar a aba Networking (Rede)

Clique em **"Next: Networking >"** para avançar. Na aba **"Networking"**, verifique e ajuste:

- **Virtual network (Rede virtual):** O Azure criará automaticamente uma nova VNet — mantenha o nome sugerido (ex: `(new) lab-vm-rg-vnet`)
- **Subnet (Sub-rede):** Mantenha a sub-rede padrão sugerida (ex: `(new) default (10.0.0.0/24)`)
- **Public IP (IP público):** Mantenha **`(new) lab-vm-01-ip`** — será criado um IP público automaticamente
- **NIC network security group (Grupo de segurança de rede da NIC):** Mantenha **`Basic`**
- **Public inbound ports (Portas de entrada públicas):** Mantenha **`Allow selected ports`**
- **Select inbound ports:** Confirme que **`SSH (22)`** está selecionado
- **Delete public IP and NIC when VM is deleted:** Mantenha **marcado** ✔️

> - **Virtual network (VNet):** É a rede privada isolada no Azure onde a VM será conectada. O Azure cria automaticamente uma nova VNet com o espaço de endereço padrão `10.0.0.0/16`.
> - **Subnet:** É uma subdivisão da VNet. A sub-rede padrão `10.0.0.0/24` comporta até 251 endereços IP utilizáveis.
> - **Public IP:** Permite acesso à VM pela internet. Sem ele, você não conseguiria conectar via SSH de fora do Azure.
> - **NIC network security group (NSG):** Funciona como um firewall virtual. A opção `Basic` cria regras simples baseadas nas portas selecionadas. O Azure configurará automaticamente uma regra permitindo tráfego SSH na porta 22.
> - **Delete public IP and NIC when VM is deleted:** Garante que os recursos de rede sejam removidos junto com a VM, evitando custos com recursos órfãos.

---

## 7. Avançar pelas abas restantes e adicionar Tags

Clique em **"Next: Management >"** e mantenha todos os valores padrão. Clique em **"Next: Monitoring >"** e mantenha os valores padrão. Clique em **"Next: Advanced >"** e mantenha os valores padrão. Clique em **"Next: Tags >"** e adicione as seguintes tags:

| Name (Nome) | Value (Valor) |
|---|---|
| `Ambiente` | `Lab` |
| `Projeto` | `TechChallenge` |

> - **Management:** Contém opções como desligamento automático, backup e atualização do SO. Os padrões são suficientes para um lab.
> - **Monitoring:** Configura diagnósticos de boot e monitoramento. O padrão habilita diagnóstico de boot com conta de armazenamento gerenciada.
> - **Advanced:** Permite adicionar extensões, scripts de inicialização (cloud-init) e configurações de proximidade. Não necessário para este lab.
> - **Tags:** Pares de chave-valor para organizar recursos. Usamos `Ambiente: Lab` e `Projeto: TechChallenge` para identificar que este recurso pertence ao laboratório.

---

## 8. Revisar e Criar a Virtual Machine

Clique na aba **"Review + create"** (Revisar + criar). O Azure validará todas as configurações. Confira o resumo exibido na tela, incluindo:

- **Resource group:** `lab-vm-rg`
- **Virtual machine name:** `lab-vm-01`
- **Region:** `Brazil South`
- **Image:** `Ubuntu Server 24.04 LTS - x64 Gen2`
- **Size:** `Standard_B1s`
- **Administrator account:** `azureuser` (Password)
- **OS disk type:** `Standard SSD`

Se a validação mostrar **"Validation passed"** (Validação aprovada), clique no botão **"Create"** (Criar). O deployment levará de 1 a 3 minutos.

> A etapa de **Review + create** consolida todas as configurações das abas anteriores e executa uma validação automática. O Azure verifica se os recursos solicitados estão disponíveis na região, se a cota da assinatura comporta os recursos e se não há erros de configuração. Após clicar em "Create", o Azure provisiona a VM e todos os recursos associados (disco, NIC, IP público, VNet, NSG). Acompanhe o progresso na página de deployment.

---

## 9. Verificar a VM criada

Após a mensagem **"Your deployment is complete"** (Sua implantação foi concluída), clique em **"Go to resource"** (Ir para o recurso). Na página da VM, verifique:

1. **Status:** Deve mostrar **`Running`** (Em execução)
2. **Public IP address:** Anote o endereço IP público exibido (ex: `20.201.x.x`)
3. **Overview:** Confira nome, região, tamanho, sistema operacional e grupo de recursos
4. No menu lateral, clique em **"Properties"** para ver todos os detalhes da VM

> A página **Overview** da VM mostra informações essenciais: status de execução, IP público e privado, tamanho, imagem do SO e métricas básicas de uso. O **IP público** é o endereço que você usaria para conectar via SSH (`ssh azureuser@<ip-publico>`). O status **Running** confirma que a VM foi provisionada com sucesso e o sistema operacional está inicializado.

---

## 10. Limpeza dos recursos

Para evitar custos, vamos excluir o **Resource Group inteiro**, que removerá automaticamente a VM e todos os recursos associados (disco, NIC, IP público, VNet, NSG):

1. Na barra de pesquisa do portal, digite **"Resource groups"** e clique no resultado
2. Na lista, localize e clique em **`lab-vm-rg`**
3. Clique no botão **"Delete resource group"** (Excluir grupo de recursos) no topo da página
4. No campo de confirmação, digite o nome do Resource Group: **`lab-vm-rg`**
5. Marque a opção **"Apply force delete for selected virtual machines and virtual machine scale sets"** se disponível
6. Clique no botão **"Delete"** (Excluir) para confirmar

> **Excluir o Resource Group é a forma mais segura e completa de limpar todos os recursos de um lab.** Ao excluir o grupo `lab-vm-rg`, o Azure remove automaticamente: a VM (`lab-vm-01`), o disco do SO, a placa de rede (NIC), o IP público, a rede virtual (VNet) e o grupo de segurança de rede (NSG). Isso evita que recursos órfãos continuem gerando custos. A exclusão pode levar de 2 a 5 minutos. O Azure pede a digitação do nome como confirmação para evitar exclusões acidentais.

---
