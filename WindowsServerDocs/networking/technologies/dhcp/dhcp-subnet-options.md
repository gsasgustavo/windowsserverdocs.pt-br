---
title: Opções de seleção de sub-rede DHCP
description: Este tópico fornece informações sobre opções de seleção de sub-rede DHCP para o protocolo DHCP no Windows Server 2016.
manager: dougkim
ms.topic: how-to
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: lizross
author: eross-msft
ms.date: 08/17/2018
ms.openlocfilehash: 076ca8c41616b77cb7503ca960667771c8f6f412
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948792"
---
# <a name="dhcp-subnet-selection-options"></a>Opções de seleção de sub-rede DHCP

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para obter informações sobre as novas opções de seleção de sub-rede do DHCP.

O DHCP agora dá suporte à opção 82 \( sub-opção 5 \) . Você pode usar essas opções para permitir que clientes proxy DHCP e agentes de retransmissão solicitem um endereço IP para uma sub-rede específica e de um intervalo de endereços IP e escopo específicos.  Para obter mais detalhes, confira a **opção 82 sub Option 5**: [RFC 3527 link Selection suboption para a opção de informações do agente de retransmissão para o DHCPv4](https://tools.ietf.org/html/rfc3527).

Se você estiver usando um agente de retransmissão DHCP configurado com a opção de DHCP 82, a subopção 5, o agente de retransmissão poderá solicitar uma concessão de endereço IP para clientes DHCP de um intervalo de endereços IP específico.


## <a name="option-82-sub-option-5-link-selection-sub-option"></a>Opção 82 sub opção 5: opção de seleção de link

A subopção seleção de link do agente de retransmissão permite que um agente de retransmissão DHCP especifique uma sub-rede IP da qual o servidor DHCP deve atribuir endereços IP e opções.

Normalmente, os agentes de retransmissão DHCP dependem do campo GIADDR do endereço IP do gateway \( \) para se comunicar com os servidores DHCP. No entanto, o GIADDR é limitado por suas duas funções operacionais:

1. Para informar ao servidor DHCP sobre a sub-rede na qual o cliente DHCP que está solicitando a concessão de endereço IP reside.
2. Para informar o servidor DHCP do endereço IP a ser usado para se comunicar com o agente de retransmissão.

Em alguns casos, o endereço IP que o agente de retransmissão usa para se comunicar com o servidor DHCP pode ser diferente do intervalo de endereços IP do qual o endereço IP do cliente DHCP precisa ser alocado.

A opção de seleção de link da opção 82 é útil nessa situação, permitindo que o agente de retransmissão declare explicitamente a sub-rede da qual deseja o endereço IP alocado na forma de DHCP v4 Option 82 sub Option 5.

> [!NOTE]
>
> Todos os endereços IP do agente de retransmissão (GIADDR) devem fazer parte de um intervalo de endereços IP de escopo DHCP ativo. Qualquer GIADDR fora dos intervalos de endereços IP do escopo DHCP é considerado uma retransmissão não autorizada e o servidor DHCP do Windows não reconhecerá as solicitações de cliente DHCP desses agentes de retransmissão.
>
> Um escopo especial pode ser criado para "autorizar" agentes de retransmissão. Crie um escopo com o GIADDR (ou vários se os GIADDR forem endereços IP sequenciais), exclua os endereços GIADDR da distribuição e, em seguida, ative o escopo. Isso autorizará os agentes de retransmissão ao impedir que os endereços GIADDR sejam atribuídos.


### <a name="use-case-scenario"></a>Cenário do caso de uso

Nesse cenário, uma rede de organização inclui um servidor DHCP e um AP de ponto de acesso sem fio \( \) para os usuários convidados. Os endereços IP do cliente de convidados são atribuídos do servidor DHCP da organização-no entanto, devido a restrições de política de firewall, o servidor DHCP não pode acessar a rede sem fio convidada ou clientes sem fio com mensagens broadcase.

Para resolver essa restrição, o AP é configurado com a subopção de seleção de link 5 para especificar a sub-rede da qual ele deseja o endereço IP alocado para clientes convidados, enquanto no GIADDR também especifica o endereço IP da interface interna que leva à rede corporativa.
