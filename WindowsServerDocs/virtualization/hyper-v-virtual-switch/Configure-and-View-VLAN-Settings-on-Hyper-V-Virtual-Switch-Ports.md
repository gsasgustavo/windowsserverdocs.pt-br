---
title: Configurar e exibir configurações de VLAN em Portas de comutador virtual do Hyper-V
description: Você pode usar este tópico para aprender as práticas recomendadas para configurar e exibir as configurações de rede local virtual (VLAN) em uma porta do comutador virtual do Hyper-V no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 69e0e28a-98ae-4ade-bd27-ce2ad7eb310f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 85d622094ac81aea8a2d90e4ef6eb5d226d0b290
ms.sourcegitcommit: 50b295002d60f4183f452cc169f0768a347830ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91248579"
---
# <a name="configure-and-view-vlan-settings-on-hyper-v-virtual-switch-ports"></a>Configurar e exibir configurações de VLAN em Portas de comutador virtual do Hyper-V

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para aprender as práticas recomendadas para configurar e exibir as configurações de rede local virtual (VLAN) em uma porta de comutador virtual do Hyper-V.

Quando desejar definir as configurações de VLAN em portas do comutador virtual Hyper-V, você poderá usar o Windows &reg; Server 2016 Hyper-v Manager ou o System Center Virtual Machine Manager (VMM).

Se você estiver usando o VMM, o VMM usará o seguinte comando do Windows PowerShell para configurar a porta do comutador.

```powershell
Set-VMNetworkAdapterIsolation <VM-name|-ManagementOS -IsolationMode VLAN -DefaultIsolationID <vlan-value> -AllowUntaggedTraffic $True
```
Se você não estiver usando o VMM e estiver configurando a porta do comutador no Windows Server, poderá usar o console do Gerenciador do Hyper-V ou o seguinte comando do Windows PowerShell.
```powershell
Set-VMNetworkAdapterVlan <VM-name|-managementOS> -Access -VlanID <vlan-value>
```

Por causa desses dois métodos para definir as configurações de VLAN em portas do comutador virtual do Hyper-V, é possível que, quando você tentar exibir as configurações de porta do comutador, ele pareça que as configurações de VLAN não estejam configuradas, mesmo quando elas estiverem configuradas.

## <a name="use-the-same-method-to-configure-and-view-switch-port-vlan-settings"></a>Use o mesmo método para configurar e exibir as configurações de VLAN de porta de comutador

Para garantir que você não encontre esses problemas, você deve usar o mesmo método para exibir as configurações de VLAN de porta do comutador que usou para definir as configurações de VLAN de porta do comutador.

Para configurar e exibir as configurações de porta do comutador de VLAN, você deve fazer o seguinte:

- Se você estiver usando o VMM ou o controlador de rede para configurar e gerenciar sua rede e tiver implantado SDN (rede definida pelo software), deverá usar os cmdlets **VMNetworkAdapterIsolation** .
- Se você estiver usando o Gerenciador do Hyper-V do Windows Server 2016 ou cmdlets do Windows PowerShell e não tiver implantado o SDN (rede definida pelo software), deverá usar os cmdlets **VMNetworkAdapterVlan** .

### <a name="possible-issues"></a>Possíveis problemas

Se você não seguir essas diretrizes, poderá encontrar os seguintes problemas.

- Em circunstâncias em que você implantou o SDN e usa o VMM, o controlador de rede ou os cmdlets **VMNetworkAdapterIsolation** para definir as configurações de VLAN em uma porta do comutador virtual do Hyper-v: se você usar o Gerenciador do Hyper-v ou **obter VMNetworkAdapterVlan** para exibir as definições de configuração, a saída do comando não exibirá as configurações de VLAN. Em vez disso, você deve usar o cmdlet **Get-VMNetworkIsolation** para exibir as configurações de VLAN.
- Em circunstâncias em que você não implantou o SDN e, em vez disso, usa o Gerenciador do Hyper-V ou os cmdlets **VMNetworkAdapterVlan** para definir as configurações de VLAN em uma porta do comutador virtual do Hyper-v: se você usar o cmdlet **Get-VMNetworkIsolation** para exibir as definições de configuração, a saída do comando não exibirá as configurações de VLAN. Em vez disso, você deve usar o cmdlet **Get VMNetworkAdapterVlan** para exibir as configurações de VLAN.

Também é importante não tentar definir as mesmas configurações de VLAN de porta de comutador usando ambos os métodos de configuração. Se você fizer isso, a porta do comutador será configurada incorretamente e o resultado poderá ser uma falha na comunicação de rede.

### <a name="resources"></a>Recursos

Para obter mais informações sobre os comandos do Windows PowerShell mencionados neste tópico, consulte o seguinte:

- [Set-VmNetworkAdapterIsolation](/powershell/module/hyper-v/set-vmnetworkadapterisolation?view=win10-ps)
- [Get-VmNetworkAdapterIsolation](/powershell/module/hyper-v/get-vmnetworkadapterisolation?view=win10-ps)
- [Set-VMNetworkAdapterVlan](/powershell/module/hyper-v/set-vmnetworkadaptervlan?view=win10-ps)
- [Get-VMNetworkAdapterVlan](/powershell/module/hyper-v/get-vmnetworkadaptervlan?view=win10-ps)
