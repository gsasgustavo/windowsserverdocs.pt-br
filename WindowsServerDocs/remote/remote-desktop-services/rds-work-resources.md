---
title: Personalizar o título "Recursos de trabalho" do RDS usando o PowerShell no Windows Server
description: Fornece a descrição de como alterar o nome do workspace no Windows Server.
ms.author: helohr
ms.date: 10/26/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: cbcd6711b183b9a57309e72bf43c4b23fd135af4
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96866235"
---
# <a name="customize-the-rds-title-work-resources-using-powershell-on-windows-server"></a>Personalizar o título "Recursos de trabalho" do RDS usando o PowerShell no Windows Server

Ao usar o Windows Server para acessar RemoteApps ou áreas de trabalho pelo WebAccess da Área de Trabalho Remota ou o novo aplicativo de Área de Trabalho Remota, você talvez tenha observado que o workspace se chama &quot;Recursos de Trabalho&quot; por padrão.  Você pode alterar facilmente o título usando cmdlets do PowerShell.

Para alterar o título, abra uma nova janela do PowerShell no servidor do agente de conexão e importe o módulo RemoteDesktop com o comando a seguir.

```powershell
    Import-Module RemoteDesktop
```

Use o comando Set-RDWorkspace para alterar o nome do espaço de trabalho.

```powershell
    Set-RDWorkspace [-Name] <string> [-ConnectionBroker <string>]  [<CommonParameters>]
```

Por exemplo, você pode usar o comando a seguir para alterar o nome do espaço de trabalho para "Contoso RemoteApps":

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker broker01.contoso.com
```

Se estiver executando vários Agentes de Conexão no modo de Alta Disponibilidade, você deverá executá-lo no agente ativo. Você pode usar este comando:

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker (Get-RDConnectionBrokerHighAvailability).ActiveManagementServer
```

Para saber mais sobre o cmdlet Set-RDWorkspace, confira a referência [Set-RDSWorkspace](/powershell/module/remotedesktop/set-rdworkspace).
