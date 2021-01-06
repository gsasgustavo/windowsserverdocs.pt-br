---
title: Guia de cenários de política de DNS
description: Saiba como usar a política DNS para controlar como um servidor DNS processa consultas de resolução de nomes com base em parâmetros diferentes que você define em políticas.
manager: brianlic
ms.topic: article
ms.assetid: 50fdb08a-bbd8-4107-954a-6699672110ff
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 49a928ab46bc190af279b17eaa23ca0ae04869b5
ms.sourcegitcommit: 029b1e19ce11160d5f988046e04a83e8ab5a60dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97904621"
---
# <a name="dns-policy-scenario-guide"></a>Guia de cenários de política de DNS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Este guia destina-se ao uso por administradores de DNS, rede e sistemas.

A política DNS é um novo recurso para DNS no Windows Server &reg; 2016. Você pode usar este guia para aprender a usar a política DNS para controlar como um servidor DNS processa consultas de resolução de nomes com base em parâmetros diferentes que você define em políticas.

Este guia contém informações de visão geral da política DNS, bem como cenários de política DNS específicos que fornecem instruções sobre como configurar o comportamento do servidor DNS para atingir suas metas, incluindo o gerenciamento de tráfego baseado na localização geográfica para servidores DNS primários e secundários, alta disponibilidade do aplicativo, DNS de divisão e muito mais.

Este guia contém as seções a seguir.

- [Visão geral das políticas de DNS](DNS-Policies-Overview.md)
- [Usar política de DNS para gerenciamento de tráfego baseado em localização geográfica com servidores primários](primary-geo-location.md)
- [Usar política de DNS para gerenciamento de tráfego baseado em localização geográfica com implantações primárias e secundárias](primary-secondary-geo-location.md)
- [Usar a política de DNS para respostas de DNS inteligente com base na hora do dia](dns-tod-intelligent.md)
- [Respostas DNS com base na hora do dia com um servidor de aplicativos de nuvem do Azure](dns-tod-azure-cloud-app-server.md)
- [Usar a política DNS para Split-Brain implantação de DNS](split-brain-DNS-deployment.md)
- [Use a política DNS para Split-Brain DNS no Active Directory](dns-sb-with-ad.md)
- [Usar a política DNS para aplicar filtros em consultas DNS](apply-filters-on-dns-queries.md)
- [Usar a Política de DNS para balanceamento de carga de aplicativo](app-lb.md)
- [Usar a Política de DNS para balanceamento de aplicativo com reconhecimento de localização geográfica](app-lb-geo.md)

