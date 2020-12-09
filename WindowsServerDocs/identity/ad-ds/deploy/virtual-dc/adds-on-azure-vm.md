---
title: Instalar o Active Directory Domain Services em uma máquina virtual do Azure
description: Como criar uma nova floresta Active Directory em uma VM (máquina virtual) em uma máquina virtual do Azure.
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 04/11/2019
ms.topic: article
ms.openlocfilehash: 3da3a66a6d414c5e80b5f84dc14c5e739a7f788a
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96866335"
---
# <a name="install-a-new-active-directory-forest-using-azure-cli"></a>Instalar uma nova floresta do Active Directory usando a CLI do Azure

AD DS pode ser executado em uma VM (máquina virtual) do Azure da mesma maneira que é executado em muitas instâncias locais. Este artigo orienta você pela implantação de uma nova floresta AD DS, em dois novos controladores de domínio, em um conjunto de disponibilidade do Azure usando o portal do Azure e CLI do Azure. Muitos clientes acham essas diretrizes úteis ao criar um laboratório ou se preparar para implantar controladores de domínio no Azure.

## <a name="components"></a>Componentes

* Um grupo de recursos no qual colocar tudo.
* Uma [rede virtual do Azure](/azure/virtual-network/virtual-networks-overview.md), uma sub-rede, um grupo de segurança de rede e uma regra para permitir o acesso RDP às VMs.
* Um [conjunto de disponibilidade](/azure/virtual-machines/windows/regions-and-availability#availability-sets) de máquina virtual do Azure para colocar dois controladores de domínio de Active Directory Domain Services (AD DS) no.
* Duas máquinas virtuais do Azure para execução AD DS e DNS.

### <a name="items-that-are-not-covered"></a>Itens que não são cobertos

* [Criando uma conexão VPN site a site a](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) partir de um local
* [Protegendo o tráfego de rede no Azure](/azure/security/azure-security-network-security-best-practices.md)
* [Criando a topologia do site](../../plan/designing-the-site-topology.md)
* [Posicionamento da função mestre de operações de planejamento](../../plan/planning-operations-master-role-placement.md)
* [Implantando Azure AD Connect para sincronizar identidades com o Azure AD](/azure/active-directory/hybrid/how-to-connect-install-express)

## <a name="build-the-test-environment"></a>Criar o ambiente de teste

Usamos o [portal do Azure](https://portal.azure.com) e [CLI do Azure](/cli/azure/overview) para criar o ambiente.

A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts. Este tutorial detalha o uso do CLI do Azure para implantar máquinas virtuais que executam o Windows Server 2019. Após a conclusão da implantação, nós nos conectamos aos servidores e instalamos AD DS.

Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free) antes de começar.

### <a name="using-azure-cli"></a>Usando a CLI do Azure

O script a seguir automatiza o processo de criação de duas VMs do Windows Server 2019, com a finalidade de criar controladores de domínio para uma nova floresta Active Directory no Azure. Um administrador pode modificar as variáveis abaixo para atender às suas necessidades e, em seguida, concluir, como uma operação. O script cria o grupo de recursos necessário, o grupo de segurança de rede com uma regra de tráfego para Área de Trabalho Remota, rede virtual e sub-rede e grupo de disponibilidade. As VMs são, cada uma, compiladas com um disco de dados de 20 GB com cache desabilitado para AD DS ser instalado no.

O script abaixo pode ser executado diretamente do portal do Azure. Se você optar por instalar e usar a CLI localmente, este guia de início rápido exigirá a execução da CLI do Azure versão 2.0.4 ou posterior. Execute `az --version` para encontrar a versão. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure](/cli/azure/install-azure-cli).

| Nome da variável | Finalidade |
| :---: | :--- |
| AdminUsername | Nome de usuário a ser configurado em cada VM como o administrador local. |
| AdminPassword | Senha de texto não criptografado a ser configurada em cada VM como a senha de administrador local. |
| ResourceGroupName | Nome a ser usado para o grupo de recursos. Não deve duplicar um nome existente. |
| Localização | Nome do local do Azure no qual você deseja implantar. Listar regiões com suporte para a assinatura atual usando `az account list-locations` . |
| VNetName | O nome para atribuir a rede virtual do Azure não deve duplicar um nome existente. |
| VNetAddress | Escopo de IP a ser usado para a rede do Azure. Não deve duplicar um intervalo existente. |
| SubnetName | Nome para atribuir a sub-rede IP. Não deve duplicar um nome existente. |
| SubnetAddress | Endereço de sub-rede para os controladores de domínio. Deve ser uma sub-rede dentro da VNet. |
| AvailabilitySet | Nome do conjunto de disponibilidade em que as VMs do controlador de domínio ingressarão. |
| VMSize | Tamanho de VM do Azure padrão disponível no local para implantação. |
| Datadisks | Tamanho em GB para o disco de dados onde AD DS é instalado. |
| DomainController1 | Nome do primeiro controlador de domínio. |
| DC1IP | Endereço IP do primeiro controlador de domínio. |
| DomainController2 | Nome do segundo controlador de domínio. |
| DC2IP | Endereço IP do segundo controlador de domínio. |

```azurecli
#Update based on your organizational requirements
Location=westus2
ResourceGroupName=ADonAzureVMs
NetworkSecurityGroup=NSG-DomainControllers
VNetName=VNet-AzureVMsWestUS2
VNetAddress=10.10.0.0/16
SubnetName=Subnet-AzureDCsWestUS2
SubnetAddress=10.10.10.0/24
AvailabilitySet=DomainControllers
VMSize=Standard_DS1_v2
DataDiskSize=20
AdminUsername=azureuser
AdminPassword=ChangeMe123456
DomainController1=AZDC01
DC1IP=10.10.10.11
DomainController2=AZDC02
DC2IP=10.10.10.12

# Create a resource group.
az group create --name $ResourceGroupName \
                --location $Location

# Create a network security group
az network nsg create --name $NetworkSecurityGroup \
                      --resource-group $ResourceGroupName \
                      --location $Location

# Create a network security group rule for port 3389.
az network nsg rule create --name PermitRDP \
                           --nsg-name $NetworkSecurityGroup \
                           --priority 1000 \
                           --resource-group $ResourceGroupName \
                           --access Allow \
                           --source-address-prefixes "*" \
                           --source-port-ranges "*" \
                           --direction Inbound \
                           --destination-port-ranges 3389

# Create a virtual network.
az network vnet create --name $VNetName \
                       --resource-group $ResourceGroupName \
                       --address-prefixes $VNetAddress \
                       --location $Location \

# Create a subnet
az network vnet subnet create --address-prefix $SubnetAddress \
                              --name $SubnetName \
                              --resource-group $ResourceGroupName \
                              --vnet-name $VNetName \
                              --network-security-group $NetworkSecurityGroup

# Create an availability set.
az vm availability-set create --name $AvailabilitySet \
                              --resource-group $ResourceGroupName \
                              --location $Location

# Create two virtual machines.
az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController1 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC1IP \
    --no-wait

az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController2 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC2IP
```

## <a name="dns-and-active-directory"></a>DNS e Active Directory

Se as máquinas virtuais do Azure criadas como parte desse processo forem uma extensão de uma infraestrutura de Active Directory local existente, as configurações de DNS na rede virtual deverão ser alteradas para incluir seus servidores DNS locais antes da implantação. Esta etapa é importante para permitir que os controladores de domínio recém-criados no Azure resolvam recursos locais e permitam que a replicação ocorra. Mais informações sobre DNS, Azure e como definir configurações podem ser encontradas na seção [resolução de nomes que usa seu próprio servidor DNS](/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#name-resolution-that-uses-your-own-dns-server).

Depois de promover os novos controladores de domínio no Azure, eles precisarão ser definidos para os servidores DNS primários e secundários para a rede virtual, e quaisquer servidores DNS locais serão rebaixados para o terciário e posterior. Mais informações sobre como alterar servidores DNS podem ser encontradas no artigo [criar, alterar ou excluir uma rede virtual](/azure/virtual-network/manage-virtual-network#change-dns-servers).

Informações sobre como estender uma rede local para o Azure podem ser encontradas no artigo [criando uma conexão VPN site a site](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal).

## <a name="configure-the-vms-and-install-active-directory-domain-services"></a>Configurar as VMs e instalar Active Directory Domain Services

Depois que o script for concluído, navegue até o [portal do Azure](https://portal.azure.com)e, em seguida, **máquinas virtuais**.

### <a name="configure-the-first-domain-controller"></a>Configurar o primeiro controlador de domínio

Conecte-se ao AZDC01 usando as credenciais fornecidas no script.

* Inicialize e formate o disco de dados como F:
   * Abra o menu iniciar e navegue até **Gerenciamento do computador**
   * Navegue até **Storage**  >  **Gerenciamento de disco** de armazenamento
   * Inicializar o disco como MBR
   * Criar um novo volume simples e atribuir a letra da unidade F: você pode fornecer um rótulo de volume, se desejar
* Instalar Active Directory Domain Services usando Gerenciador do Servidor
* Promover o controlador de domínio como o primeiro em uma nova floresta
   * Deixe o servidor DNS (sistema de nomes de domínio) e o GC (catálogo global) marcados na página de opções do controlador de domínio
   * Especificar uma senha de Modo de Restauração dos Serviços de Diretório com base em seus requisitos organizacionais
   * Altere os caminhos de C: para apontar para a unidade F: que criamos quando solicitado para sua localização
   * Examine as seleções feitas no assistente e escolha **Avançar**

> [!NOTE]
> A verificação de pré-requisitos avisará que o adaptador de rede física não tem endereços IP estáticos atribuídos, você pode ignorá-lo com segurança, pois os IPs estáticos são atribuídos na rede virtual do Azure.

* Escolha **instalar**

Quando o assistente conclui o processo de instalação, a VM é reiniciada.

Quando a VM tiver concluído a reinicialização, faça logon novamente com as credenciais usadas antes, mas desta vez como um membro do domínio que você criou.

   > [!NOTE]
   > O primeiro logon após a promoção para um controlador de domínio pode levar mais tempo do que o normal e isso é OK. Pegue uma xícara de chá, café, água ou outra bebida de escolha.

As [redes virtuais do Azure agora dão suporte ao IPv6](/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6) , mas, caso você queira definir suas VMs para preferir IPv4 sobre IPv6, as informações sobre como concluir essa tarefa podem ser encontradas no artigo [orientação da base de dados de conhecimento para configurar o IPv6 no Windows para usuários avançados](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users).

### <a name="configure-dns"></a>Configurar DNS

Depois de promover o primeiro servidor no Azure, os servidores precisarão ser definidos para os servidores DNS primários e secundários para a rede virtual, e quaisquer servidores DNS locais serão rebaixados para terciário e posterior. Mais informações sobre como alterar servidores DNS podem ser encontradas no artigo [criar, alterar ou excluir uma rede virtual](/azure/virtual-network/manage-virtual-network#change-dns-servers).

### <a name="configure-the-second-domain-controller"></a>Configurar o segundo controlador de domínio

Conecte-se ao AZDC02 usando as credenciais fornecidas no script.

* Inicialize e formate o disco de dados como F:
   * Abra o menu iniciar e navegue até **Gerenciamento do computador**
   * Navegue até **Storage**  >  **Gerenciamento de disco** de armazenamento
   * Inicializar o disco como MBR
   * Criar um novo volume simples e atribuir a letra da unidade F: (você pode fornecer um rótulo de volume, se desejar)
* Instalar Active Directory Domain Services usando Gerenciador do Servidor
* Promover o controlador de domínio
   * Adicionar um controlador de domínio a um domínio existente-CONTOSO.com
   * Fornecer credenciais para executar a operação
   * Altere os caminhos de C: para apontar para a unidade F: que criamos quando solicitado para sua localização
   * Verifique se o servidor DNS (sistema de nomes de domínio) e o GC (catálogo global) estão marcados na página Opções do controlador de domínio
   * Especificar uma senha de Modo de Restauração dos Serviços de Diretório com base em seus requisitos organizacionais
   * Examine as seleções feitas no assistente e escolha **Avançar**

> [!NOTE]
> A verificação de pré-requisitos avisará que o adaptador de rede física não tem endereços IP estáticos atribuídos. Você pode ignorá-lo com segurança, pois os IPs estáticos são atribuídos na rede virtual do Azure.

* Escolha **instalar**

Quando o assistente conclui o processo de instalação, a VM é reiniciada.

Quando a VM tiver concluído a reinicialização, faça logon novamente com as credenciais usadas antes, mas desta vez como um membro do domínio CONTOSO.com

As [redes virtuais do Azure agora dão suporte ao IPv6](/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6), mas, caso você queira definir suas VMs para preferir IPv4 sobre IPv6, as informações sobre como concluir essa tarefa podem ser encontradas no artigo [orientação da base de dados de conhecimento para configurar o IPv6 no Windows para usuários avançados](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users).

### <a name="wrap-up"></a>Conclusão

Neste ponto, o ambiente tem um par de controladores de domínio e configuramos a rede virtual do Azure para que os servidores adicionais possam ser adicionados ao ambiente. As tarefas pós-instalação para Active Directory Domain Services, como configurar sites e serviços, auditar, fazer backup e proteger a conta interna de administrador, devem ser concluídas neste ponto.

## <a name="removing-the-environment"></a>Removendo o ambiente

Para remover o ambiente, quando você tiver concluído o teste, o grupo de recursos criado acima poderá ser excluído. Esta etapa remove todos os componentes que fazem parte desse grupo de recursos.

### <a name="remove-using-the-azure-portal"></a>Remover usando o portal do Azure

No portal do Azure, navegue até **grupos de recursos** e escolha o grupo de recursos que criamos (neste exemplo ADonAzureVMs) e, em seguida, selecione **excluir grupo de recursos**. O processo solicita confirmação antes de excluir todos os recursos contidos no grupo de recursos.

### <a name="remove-using-the-azure-cli"></a>Remover usando o CLI do Azure

Em CLI do Azure execute o seguinte comando:

```azurecli
az group delete --name ADonAzureVMs
```

## <a name="next-steps"></a>Próximas etapas

* [Virtualização com segurança do AD DS (Active Directory Domain Services)](../../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)
* [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect-get-started-express)
* [Backup e recuperação](/azure/virtual-machines/windows/backup-recovery)
* [Conectividade VPN site a site](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Monitoring](/azure/virtual-machines/windows/monitor)
* [Segurança e política](/azure/virtual-machines/windows/security-policy)
* [Manutenção e atualizações](/azure/virtual-machines/windows/maintenance-and-updates)
