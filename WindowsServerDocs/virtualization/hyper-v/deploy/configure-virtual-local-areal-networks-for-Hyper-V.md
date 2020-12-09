---
title: Configurar redes locais virtuais para o Hyper-V
description: Fornece instruções para configurar uma rede de área local virtual (VLAN) para uso por máquinas virtuais em um host Hyper-V.
ms.topic: article
ms.assetid: 8510a709-001c-4eee-b6d6-c451e8a8a836
ms.author: benarm
author: BenjaminArmstrong
ms.date: 10/11/2016
ms.openlocfilehash: 22f9890fd1a3a90fcbab59a9ed1de8481e117e75
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96866155"
---
# <a name="configure-virtual-local-area-networks-for-hyper-v"></a>Configurar redes locais virtuais para o Hyper-V
As \( VLANs de redes locais virtuais \) oferecem uma maneira de isolar o tráfego de rede. As VLANs são configuradas em switches e roteadores que dão suporte a 802.1 q. Se você configurar várias VLANs e quiser que a comunicação ocorra entre elas, será necessário configurar os dispositivos de rede para permitir isso.

Você precisará do seguinte para configurar VLANs:

- Um adaptador de rede física e um driver que dá suporte à marcação de VLAN 802.1 q.
- Um comutador de rede física que dá suporte à marcação de VLAN 802.1 q.

No host, você configurará o comutador virtual para permitir o tráfego de rede na porta do comutador físico. Isso é para as IDs de VLAN que você deseja usar internamente com máquinas virtuais. Em seguida, configure a máquina virtual para especificar a VLAN que será usada pela máquina virtual para todas as comunicações de rede.

#### <a name="to-allow-a-virtual-switch-to-use-a-vlan"></a>Para permitir que um comutador virtual use uma VLAN

1. Abra o \- Gerenciador do Hyper V.

2. No menu Ações , clique em **Gerenciador do Comutador Virtual**.

3. Em **comutadores virtuais**, selecione um comutador virtual conectado a um adaptador de rede física que dá suporte a VLANs.

4. No painel direito, em ID de VLAN, selecione **habilitar identificação de LAN virtual** e digite um número para a ID de VLAN.

    Todo o tráfego que passa pelo adaptador de rede física conectado ao comutador virtual será marcado com a ID de VLAN definida.

#### <a name="to-allow-a-virtual-machine-to-use-a-vlan"></a>Para permitir que uma máquina virtual use uma VLAN

1. Abra o \- Gerenciador do Hyper V.

2. No painel de resultados, em **máquinas virtuais**, selecione a máquina virtual apropriada e clique com o botão direito do mouse em **configurações**.

3. Em **hardware**, selecione um comutador virtual que é configurado com uma VLAN.

4. No painel direito, selecione **habilitar identificação de LAN virtual** e digite a mesma ID de VLAN que você especificou para o comutador virtual.

Se a máquina virtual precisar usar mais VLANs, siga um destes procedimentos:

- Conecte mais adaptadores de rede virtual a comutadores virtuais apropriados e atribua as IDs de VLAN. Certifique-se de configurar os endereços IP corretamente e que o tráfego que você deseja rotear por meio da VLAN também usa o endereço IP correto.

- Configure o adaptador de rede virtual no modo de tronco usando o cmdlet [set \- VMNetworkAdapterVlan](/powershell/module/hyper-v/set-vmnetworkadaptervlan) .

## <a name="see-also"></a>Consulte Também

[\-Comutador virtual Hyper-V](../../hyper-v-virtual-switch/hyper-v-virtual-switch.md)
