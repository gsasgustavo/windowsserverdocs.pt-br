---
title: Configure emparelhamento de rede virtual
description: A configuração do emparelhamento de rede virtual envolve a criação de duas redes virtuais que são emparelhadas.
manager: grcusanz
ms.topic: how-to
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/08/2018
ms.openlocfilehash: 5a4468da9121c541cd87a037bea9f94da1cc582d
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716582"
---
# <a name="configure-virtual-network-peering"></a>Configure emparelhamento de rede virtual

>Aplica-se a: Windows Server 2019, Windows Server 2016

Neste procedimento, você usa o Windows PowerShell para criar duas redes virtuais, cada uma com uma sub-rede. Em seguida, você configura o emparelhamento entre as duas redes virtuais para habilitar a conectividade entre elas.

- [Etapa 1. Criar a primeira rede virtual](#step-1-create-the-first-virtual-network)

- [Etapa 2. Criar a segunda rede virtual](#step-2-create-the-second-virtual-network)

- [Etapa 3. Configurar o emparelhamento da primeira rede virtual para a segunda rede virtual](#step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network)

- [Etapa 4. Configurar o emparelhamento da segunda rede virtual para a primeira rede virtual](#step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network)


>[!IMPORTANT]
>Lembre-se de atualizar as propriedades do seu ambiente.

## <a name="step-1-create-the-first-virtual-network"></a>Etapa 1. Criar sua primeira rede virtual

Nesta etapa, você usa o Windows PowerShell para encontrar a rede lógica do provedor HNV para criar a primeira rede virtual com uma sub-rede. O script de exemplo a seguir cria a rede virtual da contoso com uma sub-rede.

``` PowerShell
#Find the HNV Provider Logical Network

$logicalnetworks = Get-NetworkControllerLogicalNetwork -ConnectionUri $uri
foreach ($ln in $logicalnetworks) {
   if ($ln.Properties.NetworkVirtualizationEnabled -eq "True") {
      $HNVProviderLogicalNetwork = $ln
   }
}

#Create the Virtual Subnet

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet
$vsubnet.ResourceId = "Contoso"
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties
$vsubnet.Properties.AddressPrefix = "24.30.1.0/24"
$uri=”https://restserver”

#Create the Virtual Network

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.1.0/24")
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork
$vnetproperties.Subnets = @($vsubnet)
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -Properties $vnetproperties
```

## <a name="step-2-create-the-second-virtual-network"></a>Etapa 2. Criar a segunda rede virtual

Nesta etapa, você cria uma segunda rede virtual com uma sub-rede. O script de exemplo a seguir cria a rede virtual do Woodgrove com uma sub-rede.

``` PowerShell

#Create the Virtual Subnet

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet
$vsubnet.ResourceId = "Woodgrove"
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties
$vsubnet.Properties.AddressPrefix = "24.30.2.0/24"
$uri=”https://restserver”

#Create the Virtual Network

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.2.0/24")
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork
$vnetproperties.Subnets = @($vsubnet)
New-NetworkControllerVirtualNetwork -ResourceId "Woodgrove_VNet1" -ConnectionUri $uri -Properties $vnetproperties
```

## <a name="step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network"></a>Etapa 3. Configurar o emparelhamento da primeira rede virtual para a segunda rede virtual

Nesta etapa, você configura o emparelhamento entre a primeira rede virtual e a segunda rede virtual criada nas duas etapas anteriores. O script de exemplo a seguir estabelece o emparelhamento de rede virtual de **Contoso_vnet1** para **Woodgrove_vnet1**.

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties
$vnet2 = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Woodgrove_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2

#Indicate whether communication between the two virtual networks
$peeringProperties.allowVirtualnetworkAccess = $true

#Indicates whether forwarded traffic is allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true

#Indicates whether the peer virtual network can access this virtual networks gateway
$peeringProperties.allowGatewayTransit = $false

#Indicates whether this virtual network uses peer virtual networks gateway
$peeringProperties.useRemoteGateways =$false

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Contoso_vnet1” -ResourceId “ContosotoWoodgrove” -Properties $peeringProperties

```

>[!IMPORTANT]
>Depois de criar esse emparelhamento, o status da vnet mostrará **iniciado**.

## <a name="step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network"></a>Etapa 4. Configurar o emparelhamento da segunda rede virtual para a primeira rede virtual

Nesta etapa, você configura o emparelhamento entre a segunda rede virtual e a primeira rede virtual criada nas etapas 1 e 2 acima. O script de exemplo a seguir estabelece o emparelhamento de rede virtual de **Woodgrove_vnet1** para **Contoso_vnet1**.

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties
$vnet2=Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Contoso_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2

# Indicates whether communication between the two virtual networks is allowed
$peeringProperties.allowVirtualnetworkAccess = $true

# Indicates whether forwarded traffic will be allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true

# Indicates whether the peer virtual network can access this virtual network's gateway
$peeringProperties.allowGatewayTransit = $false

# Indicates whether this virtual network will use peer virtual network's gateway
$peeringProperties.useRemoteGateways =$false

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Woodgrove_vnet1” -ResourceId “WoodgrovetoContoso” -Properties $peeringProperties

```

Depois de criar esse emparelhamento, o status de emparelhamento vnet mostra **conectado** para ambos os pares. Agora, as máquinas virtuais em uma rede virtual podem se comunicar com máquinas virtuais na rede virtual emparelhada.

---