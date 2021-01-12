---
title: Arquitetura de política de QoS
description: Saiba mais sobre a arquitetura da política de QoS.
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 68b61610a28c81141e336826229793f681276ade
ms.sourcegitcommit: d42b80f947dbfa8660d982be67d77745a28081e5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2021
ms.locfileid: "98113282"
---
# <a name="qos-policy-architecture"></a>Arquitetura de política de QoS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para saber mais sobre a arquitetura da política de QoS.

A figura a seguir mostra a arquitetura da QoS baseada em políticas.

![Arquitetura da política de QoS](../../media/QoS/QoS-Policy-Architecture.jpg)

A arquitetura da QoS baseada em políticas consiste nos seguintes componentes:

- **Política de grupo serviço de cliente**. Um serviço do Windows que gerencia configurações do usuário e do computador Política de Grupo.

- **Política de grupo mecanismo**. Um componente do serviço de cliente do Política de Grupo que recupera as configurações do usuário e do computador Política de Grupo de Active Directory na inicialização e verifica periodicamente se há alterações \( por padrão, a cada 90 minutos \) . Se forem detectadas alterações, o mecanismo de Política de Grupo recuperará as novas configurações de Política de Grupo. O mecanismo de Política de Grupo processa os GPOs de entrada e informa a extensão do lado do cliente QoS quando as políticas de QoS são atualizadas.

- **Extensão do lado do cliente QoS**. Um componente do serviço de cliente do Política de Grupo que aguarda uma indicação do mecanismo de Política de Grupo que as políticas de QoS alteraram e informam o módulo de inspeção de QoS.

- **Pilha de TCP/IP**. A pilha TCP/IP que inclui suporte integrado para IPv4 e IPv6 e dá suporte à plataforma de filtragem do Windows.

- **Inspeção de QoS**. Módulo um componente na pilha TCP/IP que aguarda indicações de alterações de política de QoS da extensão do lado do cliente de QoS, recupera as configurações da política de QoS e interage com a camada de transporte e Pacer.sys para marcar internamente o tráfego que corresponde às políticas de QoS.

- **NDIS 6. x**. Uma interface padrão entre drivers de rede de modo kernel e o sistema operacional em sistemas operacionais Windows Server e cliente. O NDIS 6. x dá suporte a filtros leves, que é um modelo de driver simplificado para drivers intermediários NDIS e drivers de miniporta que fornece melhor desempenho.

- Interface do provedor de rede de **\( QoS NPI \)**. Uma interface para drivers de modo kernel para interagir com Pacer.sys.

- **Pacer.sys**. Um driver de filtro simples do NDIS 6. x que controla o agendamento de pacotes para a QoS baseada em políticas e para o tráfego de aplicativos que usam as \( APIs de TC de controle de tráfego e GQoS de QoS genérica \) \( \) . Pacer.sys substituído Psched.sys no Windows Server 2003 e no Windows XP. O Pacer.sys é instalado com o componente de Agendador de pacotes QoS nas propriedades de uma conexão de rede ou adaptador.

Para o próximo tópico deste guia, consulte [cenários de política de QoS](qos-policy-scenarios.md).

Para o primeiro tópico deste guia, consulte [política de QoS (qualidade de serviço)](qos-policy-top.md).

