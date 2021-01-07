---
title: Configurar regras de firewall para membros não associados a domínio para permitir tráfego BranchCache
description: Saiba como configurar produtos de firewall de terceiros e configurar manualmente um computador cliente com regras de firewall que permitem que o BranchCache seja executado no modo de cache distribuído.
manager: brianlic
ms.topic: how-to
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: e53601cf7c0a2cd4d88d440aea78843222881b6b
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950302"
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>Configurar regras de firewall para membros não associados a domínio para permitir tráfego BranchCache

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar as informações neste tópico para configurar produtos de firewall de terceiros e configurar um computador cliente manualmente com regras de firewall que permitam a execução do BranchCache no modo de cache distribuído.

> [!NOTE]
> -   Se você configurou computadores cliente BranchCache usando a Diretiva de Grupo, as configurações da Diretiva de Grupo substituirão qualquer configuração manual de computadores cliente aos quais as diretivas foram aplicadas.
> -   Se você implantou o BranchCache com DirectAccess, pode usar as configurações deste tópico para configurar regras de IPsec para permitir o tráfego de BranchCache.

A associação a **Administradores** ou equivalente é o requisito mínimo para fazer essas alterações de configuração.

## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS-PCCRD]: protocolo de descoberta de cache e recuperação de conteúdo de mesmo nível
Os clientes de cache distribuído devem permitir o tráfego MS-PCCRD de entrada e de saída executado no protocolo WS-Discovery.

As configurações de firewall devem permitir o tráfego multicast, além do tráfego de entrada e de saída. Você pode usar as seguintes configurações para definir exceções de firewall para o modo de cache distribuído.

Multicast IPv4:239.255.255.250

Multicast IPv6: FF02:: C

Tráfego de entrada: porta local: 3702, porta remota: efêmera

Tráfego de saída: porta local: efêmera, porta remota: 3702

Programa:% SystemRoot% \system32\svchost.exe (serviço do BranchCache [PeerDistSvc])

## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS-PCCRR]: cache e recuperação de conteúdo de mesmo nível: protocolo de recuperação
Os clientes de cache distribuído devem permitir o tráfego MS-PCCRR de entrada e de saída executado no protocolo HTTP 1.1 conforme documentado na RFC (solicitação de comentários) 2616.

As configurações de firewall devem permitir o tráfego de entrada e de saída. Você pode usar as seguintes configurações para definir exceções de firewall para o modo de cache distribuído.

Tráfego de entrada: porta local: 80, porta remota: efêmera

Tráfego de saída: porta local: efêmera, porta remota: 80



