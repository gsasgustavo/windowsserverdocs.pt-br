---
title: Configurar servidores de conteúdo do WSUS (Windows Server Update Services)
description: Saiba como configurar os servidores de conteúdo do Windows Server Update Services (WSUS) para armazenar arquivos de atualização no computador local.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1ecd2e601a793690791451bfd39cb949bd08715f
ms.sourcegitcommit: 029b1e19ce11160d5f988046e04a83e8ab5a60dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97904431"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Configurar servidores de conteúdo do WSUS (Windows Server Update Services)

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Depois de instalar o recurso BranchCache e iniciar o serviço BranchCache, é necessário configurar os servidores do WSUS para armazenar arquivos de atualização no computador local.

Ao configurar servidores do WSUS para armazenar arquivos de atualização no computador local, os metadados de atualização e os arquivos de atualização são baixados e armazenados diretamente no servidor do WSUS. Isso garante que os computadores cliente BranchCache recebam os arquivos de atualização dos produtos da Microsoft do servidor do WSUS e não diretamente do site do Microsoft Update.

Para obter mais informações sobre a sincronização do WSUS, consulte [Configurando sincronizações de atualização](../../../administration/windows-server-update-services/manage/setting-up-update-synchronizations.md)