---
title: Entender o uso de redes virtuais e VLANs
description: Neste tópico, você aprende sobre as redes virtuais de virtualização de rede Hyper-V e como elas diferem das VLANs (redes locais virtuais). Com a virtualização de rede Hyper-V, você cria sobreposição de redes virtuais, também chamadas de redes virtuais.
manager: grcusanz
ms.topic: article
ms.assetid: 84ac2458-3fcf-4c4f-acfe-6105443dd83f
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/26/2018
ms.openlocfilehash: 58ab0a66e5f08ba9661326b418170563a56a86a4
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716652"
---
# <a name="understand-the-usage-of-virtual-networks-and-vlans"></a>Entender o uso de redes virtuais e VLANs

>Aplica-se a: Windows Server 2019, Windows Server 2016

Neste tópico, você aprende sobre as redes virtuais de virtualização de rede Hyper-V e como elas diferem das VLANs (redes locais virtuais). Com a virtualização de rede Hyper-V, você cria sobreposição de redes virtuais, também chamadas de redes virtuais.

A SDN (rede definida pelo software) no Windows Server 2016 é baseada na política de programação para sobreposição de redes virtuais em um comutador virtual do Hyper-V. Você pode criar sobreposição de redes virtuais, também chamadas de redes virtuais, com virtualização de rede Hyper-V.

Quando você implanta a virtualização de rede do Hyper-V, as redes de sobreposição são criadas encapsulando o quadro de Ethernet da camada 2 da máquina virtual do locatário original com um cabeçalho de sobreposição ou de túnel (por exemplo, VXLAN ou NVGRE) e os cabeçalhos de Ethernet de camada 2 e de IP da rede de underlay (ou física). As redes virtuais de sobreposição são identificadas por um VNI (identificador de rede virtual) de 24 bits para manter o isolamento do tráfego de locatário e para permitir endereços IP sobrepostos. O VNI é composto por uma VSID (ID de sub-rede virtual), ID de comutador lógico e ID de túnel.

Além disso, cada locatário recebe um domínio de roteamento (semelhante ao roteamento virtual e ao encaminhamento-VRF) para que vários prefixos de sub-rede virtual (cada um representado por um VNI) possam ser roteados diretamente entre si. Não há suporte para o roteamento entre locatários (ou domínio de roteamento cruzado) sem passar por um gateway.

A rede física na qual o tráfego encapsulado de cada locatário é encapsulado é representada por uma rede lógica chamada rede lógica do provedor. Essa rede lógica do provedor consiste em uma ou mais sub-redes, cada uma representada por um prefixo de IP e, opcionalmente, uma marca de VLAN 802.1 q.

Você pode criar redes lógicas e sub-redes adicionais para fins de infraestrutura para transportar o tráfego de gerenciamento, o tráfego de armazenamento, o tráfego de migração ao vivo, etc.

O Microsoft SDN não oferece suporte ao isolamento de redes de locatário usando VLANs. O isolamento de locatário é realizado unicamente usando a sobreposição de redes virtuais e encapsulamento de virtualização de rede Hyper-V.
