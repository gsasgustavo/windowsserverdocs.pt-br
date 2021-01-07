---
title: Configurar servidores de conteúdo do WSUS (Windows Server Update Services)
description: Saiba como configurar os servidores de conteúdo do Windows Server Update Services (WSUS) para armazenar arquivos de atualização no computador local.
manager: brianlic
ms.topic: how-to
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: 9e55b470df3d1fc3eed8a69d89b228d3d7b7ed70
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950402"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Configurar servidores de conteúdo do WSUS (Windows Server Update Services)

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Depois de instalar o recurso BranchCache e iniciar o serviço BranchCache, é necessário configurar os servidores do WSUS para armazenar arquivos de atualização no computador local.

Ao configurar servidores do WSUS para armazenar arquivos de atualização no computador local, os metadados de atualização e os arquivos de atualização são baixados e armazenados diretamente no servidor do WSUS. Isso garante que os computadores cliente BranchCache recebam os arquivos de atualização dos produtos da Microsoft do servidor do WSUS e não diretamente do site do Microsoft Update.

Para obter mais informações sobre a sincronização do WSUS, consulte [Configurando sincronizações de atualização](../../../administration/windows-server-update-services/manage/setting-up-update-synchronizations.md)