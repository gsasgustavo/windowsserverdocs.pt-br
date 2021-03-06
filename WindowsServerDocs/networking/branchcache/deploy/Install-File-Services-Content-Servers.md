---
title: Instalar servidores de conteúdo dos Serviços de Arquivo
description: Saiba como instalar o BranchCache para o serviço de função de arquivos de rede da função de servidor de serviços de arquivo e habilitar o BranchCache em compartilhamentos de arquivos de acordo com suas necessidades.
manager: brianlic
ms.topic: how-to
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: 57fa39120b31ea2622c3a7d997a62fa671d2455a
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949552"
---
# <a name="install-file-services-content-servers"></a>Instalar servidores de conteúdo dos Serviços de Arquivo

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Para implantar servidores de conteúdo que executam a função de servidor de Serviços de Arquivo, instale o BranchCache para o serviço de função de arquivos de rede da função de servidor de Serviços de Arquivo. Além disso, você deve habilitar o BranchCache em compartilhamentos de arquivos de acordo com suas necessidades.

Durante a configuração do servidor de conteúdo, você pode permitir a publicação do BranchCache de conteúdo para todos os compartilhamentos de arquivos ou pode selecionar um subconjunto de compartilhamentos de arquivos para publicar.

> [!NOTE]
> Quando você implanta um servidor de arquivos habilitado para BranchCache ou um servidor Web como um servidor de conteúdo, as informações de conteúdo agora são calculadas offline, bem antes de um cliente do BranchCache solicitar um arquivo. Por causa dessa melhoria, você não precisa configurar a publicação de hash para servidores de conteúdo, como fez na versão anterior do BranchCache.
>
> Essa geração automática de hash fornece um desempenho mais rápido e mais economia de largura de banda, pois as informações de conteúdo estão prontas para o primeiro cliente que solicita o conteúdo, e os cálculos já foram realizados.

Consulte os tópicos a seguir para implantar servidores de conteúdo.

-   [Configurar a função de servidor de Serviços de Arquivo](../../branchcache/deploy/Configure-the-File-Services-server-role.md)

-   [Habilitar a publicação de hash para servidores de arquivos](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)

-   [Habilitar o BranchCache em um compartilhamento de arquivos &#40;&#41;opcional ](../../branchcache/deploy/enable-bc-on-file-share.md)



