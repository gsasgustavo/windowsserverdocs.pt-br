---
title: Visão geral do cenário de Test Lab DirectAccess Cluster-NLB
description: Saiba mais sobre o cenário de laboratório de teste do cluster do DirectAccess-NLB e as três sub-redes das quais ele consiste.
manager: brianlic
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 7c4b0aac8c5d16826a5e173fb28424333887f6be
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040266"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>Visão geral do cenário de Test Lab DirectAccess Cluster-NLB

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Nesse cenário de laboratório de teste, o DirectAccess é implantado com:

-   **DC1**-um servidor configurado como um controlador de domínio, um servidor DNS (sistema de nomes de domínio) e um servidor DHCP (protocolo de configuração dinâmica de hosts).

-   **EDGE1**-um servidor na rede interna que está configurado como o primeiro servidor de acesso remoto em um cluster de servidor de acesso remoto. Este servidor tem dois adaptadores de rede; um conectado à rede interna e o outro conectado à rede externa.

-   **EDGE2**-um servidor na rede interna configurada como o segundo servidor de acesso remoto em um cluster de servidor de acesso remoto. Este servidor tem dois adaptadores de rede; um conectado à rede interna e o outro conectado à rede externa.

-   **App1**-um servidor na rede interna configurada como um servidor Web e de arquivos e como uma autoridade de certificação raiz corporativa (CA)

-   **App2**-um computador na rede interna configurada como um servidor Web e de arquivos IPv4. Este computador é usado para realçar os recursos de NAT64/DNS64.

-   **INET1**-um servidor configurado como um servidor DNS e DHCP da Internet.

-   **NAT1**-um computador cliente configurado como um dispositivo NAT (conversor de endereços de rede) usando o compartilhamento de conexão com a Internet.

-   **CLIENT1**-um computador cliente configurado como um cliente do DirectAccess que será usado para testar a conectividade do DirectAccess ao se mover entre a rede interna, a Internet simulada e uma rede doméstica.

O laboratório de teste consiste em três sub-redes que simulam o seguinte:

-   Uma rede doméstica chamada HomeNet (192.168.137.0/24) conectada à Internet por um NAT.

-   A rede externa representada pela sub-rede da Internet (131.107.0.0/24).

-   Uma rede interna chamada corpnet (10.0.0.0/24; 2001: DB8:1::/64) separada da Internet pelo servidor de acesso remoto.

Os computadores em cada sub-rede se conectam usando um Hub ou comutador virtual ou físico, conforme mostrado na figura a seguir.

![Visão geral do laboratório de teste](../../../media/Overview-of-the-Test-Lab-Scenario_5/TLG_DA_Cluster.png)



