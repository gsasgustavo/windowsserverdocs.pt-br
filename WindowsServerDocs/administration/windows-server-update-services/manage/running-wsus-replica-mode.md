---
title: Executar o modo de réplica do WSUS
description: Tópico Windows Server Update Service (WSUS) – como configurar o modo de réplica
ms.topic: article
ms.assetid: d218cd6b-3b6b-4429-913b-31d412ce3356
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1a2d16ddfbd563ae8ef1abf3829849b81e867972
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89641208"
---
# <a name="running-wsus-replica-mode"></a>Executar o modo de réplica do WSUS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Um servidor do WSUS em execução no modo de réplica herda as aprovações de atualização e grupos de computadores criados em um servidor de administração. Em um cenário que usa o modo de réplica, normalmente você tem um único servidor de administração, e um ou mais servidores WSUS de réplica subordinada se espalham por toda a organização, com base no site ou na topografia organizacional. Você aprova as atualizações e cria grupos de computadores no servidor de administração, que os servidores de modo de réplica serão espelhados. Os servidores de modo de réplica podem ser configurados somente durante a instalação do WSUS e, se você implementou esse cenário, é provável que ele seja importante em sua organização que as aprovações de atualização e grupos de computadores sejam gerenciados centralmente.

Se o servidor do WSUS estiver sendo executado no modo de réplica, você poderá executar apenas os recursos de administração limitados no servidor, que consiste principalmente em:

-   Adicionando e removendo computadores de grupos de computadores. A associação de grupo de computadores não é distribuída para servidores de réplica, somente os próprios grupos de computadores. Portanto, em um servidor de modo de réplica, você herdará os grupos de computadores que criou no servidor de administração. No entanto, os grupos de computadores ficarão vazios. Em seguida, você deve atribuir os computadores cliente que se conectam ao servidor de réplica para os grupos de computadores.

-   Configuração de um cronograma de sincronização

-   Especificando as configurações do servidor proxy

-   Especificando a origem da atualização. Pode ser um servidor que não seja o servidor de administração

-   Visualização de atualizações disponíveis

-   Monitorando atualizações, sincronização, status do computador e configurações do WSUS no servidor

-   Executando todos os relatórios padrão do WSUS disponíveis em servidores de modo de réplica



