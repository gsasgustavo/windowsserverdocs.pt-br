---
title: Implantar uma infraestrutura de rede definida pelo software
description: Este tópico fornece links para tópicos sobre como implantar uma infraestrutura de SDN (rede definida pelo software) da Microsoft usando scripts no Windows Server 2019 e 2016.
ms.topic: how-to
ms.assetid: 6c665c88-df28-4150-81d4-a47e9fa5255c
ms.date: 08/23/2018
ms.author: anpaul
author: AnirbanPaul
manager: grcusanz
ms.openlocfilehash: a9ce251488d80b4e5180d1641bc2157227d08d71
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716012"
---
# <a name="deploy-a-software-defined-network-infrastructure"></a>Implantar uma infraestrutura de rede definida pelo software

>Aplica-se a: Windows Server 2019, Windows Server 2016

Implante a infraestrutura de SDN (rede definida pelo software) da Microsoft.

Essas implantações incluem todas as tecnologias de que você precisa para uma infraestrutura totalmente funcional, incluindo HNV (virtualização de rede) do Hyper-V, controladores de rede, SLB/MUX (balanceadores de carga de software) e gateways.

## <a name="set-up-sdn-infrastructure-in-the-vmm-fabric"></a>Configurar a infraestrutura de SDN na malha do VMM




-   [Configurar uma infraestrutura SDN (rede definida pelo software) na malha do VMM](/system-center/vmm/deploy-sdn)

    Use esse método se desejar incorporar o System Center Virtual Machine Manager (VMM) para gerenciar sua infraestrutura de SDN.

## <a name="deploy-sdn-infrastructure-using-scripts"></a>Implantar a infraestrutura de SDN usando scripts

-   [Implantar uma infraestrutura de rede definida pelo software usando scripts](../../sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)

    Use esse método se você não quiser usar o VMM para gerenciar sua infraestrutura de SDN ou se tiver outro método de gerenciamento.


## <a name="deploy-individual-sdn-technologies-instead-of-an-entire-infrastructure"></a>Implante tecnologias individuais de SDN em vez de uma infraestrutura inteira
 Se você quiser implantar tecnologias SDN individuais em vez de uma infraestrutura inteira, consulte: [implantar tecnologias de rede definidas pelo software usando o Windows PowerShell](Deploy-Software-Defined-Network-Technologies-using-Windows-PowerShell.md).








## <a name="related-topics"></a>Tópicos relacionados
- [SDN (rede definida pelo software)](../software-defined-networking.md)
- [Tecnologias de SDN](../technologies/Software-Defined-Networking-Technologies.md)
- [Planejar SDN](../plan/plan-a-software-defined-network-infrastructure.md)
- [Gerenciar SDN](../manage/manage-sdn.md)
- [Segurança para SDN](../security/sdn-security-top.md)
- [Solucionar problemas de SDN](../troubleshoot/Troubleshoot-Software-Defined-Networking.md)