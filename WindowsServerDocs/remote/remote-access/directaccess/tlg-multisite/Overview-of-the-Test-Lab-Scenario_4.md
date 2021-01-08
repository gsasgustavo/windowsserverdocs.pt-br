---
title: Visão geral do cenário de Test Lab
description: Saiba mais sobre o que o DirectAccess está implantado e as quatro sub-redes que compõem o laboratório de teste.
manager: brianlic
ms.topic: article
ms.assetid: 9afeced4-1a9b-4cb3-9fc4-d7e44c675755
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 12d6868334bafba881531fd2d5cdaa99d10555f8
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040096"
---
# <a name="overview-of-the-test-lab-scenario"></a>Visão geral do cenário de Test Lab

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Nesse cenário de laboratório de teste, o DirectAccess é implantado com:

-   **DC1**-um servidor configurado como um controlador de domínio, servidor DNS e servidor DHCP para o domínio corp.contoso.com.

-   **2-DC1**-um servidor configurado como um controlador de domínio e um servidor DNS para o domínio corp2.Corp.contoso.com.

-   **EDGE1 e 2-EDGE1**-dois servidores na rede interna configurados como servidores de acesso remoto. Cada servidor tem dois adaptadores de rede; um conectado à rede interna e o outro conectado à rede externa.

-   **App1 e 2-App1**-dois servidores na rede interna configurados como servidores Web e de arquivos.

-   **App2**-um computador na rede interna configurada como um servidor Web e de arquivos IPv4. Este computador é usado para realçar os recursos de NAT64/DNS64.

-   **ROUTER1**-um servidor configurado para fornecer roteamento entre as duas redes internas corporativas.

-   **INET1**-um servidor configurado como um servidor DNS e DHCP da Internet.

-   **NAT1**-um computador cliente configurado como um dispositivo NAT (conversor de endereços de rede) usando o compartilhamento de conexão com a Internet.

-   **CLIENT1 e CLIENT2**-dois computadores cliente que são configurados como clientes DirectAccess que serão usados para testar a conectividade do DirectAccess ao se moverem entre a rede interna, a Internet simulada e uma rede doméstica. **CLIENT2** é um cliente do Windows 7 &reg;  .

O laboratório de teste consiste em quatro sub-redes que simulam o seguinte:

-   Uma rede doméstica chamada HomeNet (192.168.137.0/24) conectada à Internet por um NAT.

-   A rede externa representada pela sub-rede da Internet (131.107.0.0/24).

-   Uma rede interna chamada corpnet (10.0.0.0/24; 2001: DB8:1::/64) separada da Internet pelo servidor de acesso remoto EDGE1.

-   Uma rede interna chamada 2-Corpnet1 (10.2.0.0/24; 2001: DB8:2::/64) separada da Internet pelo servidor de acesso remoto 2-EDGE1.

Os computadores em cada sub-rede se conectam usando um Hub ou comutador virtual ou físico, conforme mostrado na figura a seguir.

![Visão geral do laboratório de teste](../../../media/Overview-of-the-Test-Lab-Scenario_4/TLG_DA_Multisite.png)



