---
title: Diretrizes gerais para solucionar problemas do DHCP
description: Este Artilce apresenta orientações gerais para solucionar problemas de DHCP.
manager: dcscontentpm
ms.date: 5/26/2020
ms.topic: troubleshooting
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 3fb1536e3993ed92820b80c9460a1bdbcc3502c4
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947652"
---
# <a name="general-guidance-to-troubleshoot-dhcp"></a>Diretrizes gerais para solucionar problemas do DHCP

Antes de começar a solucionar problemas, verifique os itens a seguir. Isso pode ajudá-lo a encontrar a causa raiz do problema.

## <a name="checklist"></a>Lista de verificação

  - Quando começou o problema?

  - Há mensagens de erro?

  - O servidor DHCP estava funcionando anteriormente ou se ele nunca funcionou?
    Se ele funcionou anteriormente, fez alguma alteração antes do problema ser iniciado. Por exemplo, uma atualização foi instalada? Foi uma alteração feita na infraestrutura?

  - O problema é persistente ou intermitente? Se for intermitente, quando ela ocorreu pela última vez?

  - As falhas de concessão de endereço ocorrem para todos os clientes ou apenas para clientes específicos, como uma sub-rede de escopo único?

  - Há clientes na mesma sub-rede de rede que o servidor DHCP?

  - Se os clientes residirem na mesma sub-rede de rede, poderão obter endereços IP?

  - Se os clientes não estiverem na mesma sub-rede de rede, os roteadores ou comutadores de VLAN configurados corretamente para ter agentes de retransmissão DHCP (também conhecidos como auxiliares de IP)?

  - O servidor DHCP é autônomo ou está configurado para alta disponibilidade, como o escopo de divisão ou failover de DHCP?

  - Verifique os dispositivos intermediários para obter recursos como VRRP/HSRP, inspeção dinâmica de ARP ou espionagem de DHCP que são conhecidos por causar problemas.
