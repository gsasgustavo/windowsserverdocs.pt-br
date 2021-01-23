---
title: Visão geral de rede de contêineres
description: Este tópico é uma visão geral da pilha de rede para contêineres do Windows e inclui links para diretrizes adicionais sobre como criar, configurar e gerenciar redes de contêineres.
manager: grcusanz
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: anpaul
author: AnirbanPaul
ms.date: 09/04/2018
ms.openlocfilehash: 2ecc240cc1886a0355b1bf1785e2f634388474bf
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716862"
---
# <a name="container-networking-overview"></a>Visão geral de rede de contêineres

>Aplica-se a: Windows Server 2019, Windows Server 2016

Neste tópico, fornecemos uma visão geral da pilha de rede para contêineres do Windows e incluímos links para orientações adicionais sobre como criar, configurar e gerenciar redes de contêineres.

Os contêineres do Windows Server são um método leve de virtualização do sistema operacional que separa aplicativos ou serviços de outros serviços que são executados no mesmo host do contêiner. Os contêineres do Windows funcionam de forma semelhante às máquinas virtuais. Quando habilitado, cada contêiner tem uma exibição separada do sistema operacional, dos processos, do sistema de arquivos, do registro e dos endereços IP, os quais você pode se conectar a redes virtuais.

Um contêiner do Windows compartilha um kernel com o host do contêiner e todos os contêineres em execução no host. Devido ao espaço de kernel compartilhado, esses contêineres exigem a mesma versão e configuração de kernel. Os contêineres fornecem isolamento de aplicativo por meio de tecnologia de isolamento de processo e namespace.

>[!IMPORTANT]
>Os contêineres do Windows não fornecem um limite de segurança hostil e não devem ser usados para isolar código não confiável.

Com os contêineres do Windows, você pode implantar um host Hyper-V, no qual você cria uma ou mais máquinas virtuais nos hosts de VM. Dentro dos hosts da VM, os contêineres são criados e o acesso à rede é por meio de um comutador virtual em execução dentro da máquina virtual. Você pode usar imagens reutilizáveis armazenadas em um repositório para implantar o sistema operacional e os serviços em contêineres. Cada contêiner tem um adaptador de rede virtual que se conecta a um comutador virtual, encaminhando o tráfego de entrada e de saída. Você pode anexar pontos de extremidade de contêiner a uma rede de host local (como NAT), a rede física ou sobreposição de rede virtual criada por meio da pilha SDN.

Para impor o isolamento entre contêineres no mesmo host, você cria um compartimento de rede para cada contêiner do Windows Server e do Hyper-V. Contêineres do Windows Server usam uma vNIC do host para se conectar ao comutador virtual. Os contêineres do Hyper-V usam uma NIC de VM sintética (não exposta à VM do utilitário) para se conectar ao comutador virtual.

## <a name="related-topics"></a>Tópicos relacionados

- [Rede de contêiner do Windows](/virtualization/windowscontainers/container-networking/architecture): saiba como criar e gerenciar redes de contêiner para implantações não sobrepostas/Sdn.

- [Conectar pontos de extremidade do contêiner a uma rede virtual de locatário](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md): saiba como criar e gerenciar redes de contêiner para sobreposição de redes virtuais com Sdn.