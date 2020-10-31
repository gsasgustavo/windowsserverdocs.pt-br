---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: Determinando o cronograma
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 9a882ab616fae5a5ab649fb5a988aa90e8bc7a9c
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93068738"
---
# <a name="determining-the-schedule"></a>Determinando o cronograma

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Você pode controlar a disponibilidade do link de site definindo um agendamento para links de site. Quando a replicação entre dois sites atravessa vários links de site, a interseção das agendas de replicação em todos os links relevantes determina a agenda de conexão entre os dois sites.

Para planejar a definição da agenda de links de site, crie duas agendas sobrepostas entre links de site que contêm controladores de domínio que se replicam diretamente entre si. Use o agendamento padrão (100-porcentagem disponível) nesses links, a menos que você queira bloquear o tráfego de replicação durante horários de pico. Ao bloquear a replicação, você dá prioridade a outro tráfego, mas também aumenta a latência de replicação.

Os controladores de domínio armazenam o tempo no UTC (tempo Universal Coordenado). As configurações de hora em agendas de objeto de link de site estão em conformidade com a hora local do site e o computador no qual a agenda está definida. Quando um controlador de domínio entra em contato com um computador que está em um site e fuso horário diferentes, o agendamento no controlador de domínio exibe a configuração de hora de acordo com a hora local do site do computador.



