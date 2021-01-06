---
title: Implantar servidores de cache hospedado (opcional)
description: Saiba como instalar e configurar servidores de cache hospedados do BranchCache localizados em filiais onde você deseja implantar o modo de cache hospedado do BranchCache.
manager: brianlic
ms.topic: how-to
ms.assetid: 96d03b42-6cd9-4905-b6a2-dc36130dd24f
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: 9ed41c9455abb2bcd9417d393206f6f6ca6bb71c
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946722"
---
# <a name="deploy-hosted-cache-servers-optional"></a>Implantar servidores de cache hospedado (opcional)

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para instalar e configurar servidores de cache hospedados do BranchCache localizados em filiais em que você deseja implantar o modo de cache hospedado do BranchCache. Com o BranchCache no Windows Server 2016, você pode implantar vários servidores de cache hospedados em uma filial.

> [!IMPORTANT]
> Essa etapa é opcional porque o modo de cache distribuído não requer um computador de servidor de cache hospedado em filiais. Se você não estiver planejando implantar o modo de cache hospedado em qualquer filial, não será necessário implantar um servidor de cache hospedado e não precisará executar as etapas neste procedimento.

Você deve ser membro de **Administradores** ou equivalente para executar este procedimento.

### <a name="to-install-and-configure-a-hosted-cache-server"></a>Para instalar e configurar um servidor de cache hospedado

1.  No computador que você deseja configurar como um servidor de cache hospedado, execute o comando a seguir em um prompt do Windows PowerShell para instalar o recurso BranchCache.

    `Install-WindowsFeature BranchCache -IncludeManagementTools`

2.  Configure o computador como um servidor de cache hospedado usando um dos seguintes comandos:

    -   Para configurar um computador não ingressado no domínio como um servidor de cache hospedado, digite o seguinte comando no prompt do Windows PowerShell e pressione ENTER.

        `Enable-BCHostedServer`

    -   Para configurar um computador ingressado no domínio como um servidor de cache hospedado e registrar um ponto de conexão de serviço no Active Directory para descoberta automática de servidor de cache hospedado por computadores cliente, digite o seguinte comando no prompt do Windows PowerShell e pressione ENTER.

        `Enable-BCHostedServer -RegisterSCP`

3.  Para verificar a configuração correta do servidor de cache hospedado, digite o seguinte comando no prompt do Windows PowerShell e pressione ENTER.

    `Get-BCStatus`

    > [!NOTE]
    > Depois de executar esse comando, na seção **HostedCacheServerConfiguration**, o valor de **HostedCacheServerIsEnabled** será **true**. Se você tiver configurado um servidor de cache hospedado associado ao domínio para registrar um SCP (ponto de conexão de serviço) em Active Directory, o valor de **HostedCacheScpRegistrationEnabled** será **true**.


