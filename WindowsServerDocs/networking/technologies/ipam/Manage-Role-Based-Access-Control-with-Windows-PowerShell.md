---
title: Gerenciar controle de acesso baseado em função com o Windows PowerShell
description: Este tópico faz parte do guia de gerenciamento do IPAM (gerenciamento de endereços IP) no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 4f13f78e-0114-4e41-9a28-82a4feccecfc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 99859a1e9f43baa969475628e743975c78ef8bff
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96866465"
---
# <a name="manage-role-based-access-control-with-windows-powershell"></a>Gerenciar controle de acesso baseado em função com o Windows PowerShell

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para aprender a usar o IPAM para gerenciar o controle de acesso baseado em função com o Windows PowerShell.

>[!NOTE]
>Para a referência de comando do IPAM do Windows PowerShell, consulte os [cmdlets IpamServer no Windows PowerShell](/powershell/module/ipamserver/).

Os novos comandos do IPAM do Windows PowerShell fornecem a capacidade de recuperar e alterar os escopos de acesso de objetos DNS e DHCP. A tabela a seguir ilustra o comando correto a ser usado para cada objeto IPAM.

|Objeto IPAM|Comando|Descrição|
|---------------|-----------|---------------|
|Servidor DNS|Get-IpamDnsServer|Esse cmdlet retorna o objeto de servidor DNS no IPAM|
|Zona do DNS|Get-IpamDnsZone|Esse cmdlet retorna o objeto de zona DNS no IPAM|
|Registro de recurso DNS|Get-IpamResourceRecord|Esse cmdlet retorna o objeto de registro de recurso de DNS no IPAM|
|Encaminhador condicional de DNS|Get-IpamDnsConditionalForwarder|Esse cmdlet retorna o objeto de encaminhador condicional DNS no IPAM|
|Servidor DHCP|Get-IpamDhcpServer|Esse cmdlet retorna o objeto de servidor DHCP no IPAM|
|Superescopo do DHCP|Get-IpamDhcpSuperscope|Esse cmdlet retorna o objeto de superescopo DHCP no IPAM|
|Escopo do DHCP|Get-IpamDhcpScope|Esse cmdlet retorna o objeto de escopo DHCP no IPAM|

No exemplo a seguir de saída de comando, o `Get-IpamDnsZone` cmdlet recupera a zona DNS **Dublin.contoso.com** .

```
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com

ZoneName             : dublin.contoso.com
ZoneType             : Forward
AccessScopePath      : \Global\Dublin
IsSigned             : False
DynamicUpdateStatus  : None
ScavengeStaleRecords : False
```

## <a name="setting-access-scopes-on-ipam-objects"></a>Definindo escopos de acesso em objetos IPAM
Você pode definir escopos de acesso em objetos IPAM usando o `Set-IpamAccessScope` comando. Você pode usar esse comando para definir o escopo de acesso para um valor específico para um objeto ou fazer com que os objetos herdem o escopo de acesso de objetos pai. A seguir estão os objetos que você pode configurar com este comando.

-   Escopo do DHCP

-   Servidor DHCP

-   Superescopo do DHCP

-   Encaminhador condicional de DNS

-   Registros de recursos de DNS

-   Servidor DNS

-   Zona do DNS

-   Bloco de endereço IP

-   Intervalo de endereços IP

-   Espaço de endereço IP

-   Sub-rede de endereço IP

Veja a seguir a sintaxe do `Set-IpamAccessScope` comando.

```
NAME
    Set-IpamAccessScope

SYNTAX
    Set-IpamAccessScope [-IpamRange] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Set-IpamAccessScope [-IpamDnsServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDhcpServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDhcpSuperscope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDhcpScope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDnsConditionalForwarder] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDnsResourceRecord] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDnsZone] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamAddressSpace] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamSubnet] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Set-IpamAccessScope [-IpamBlock] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

No exemplo a seguir, o escopo de acesso da zona DNS **Dublin.contoso.com** é alterado de **Dublin** para **Europa**.

```
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com

ZoneName             : dublin.contoso.com
ZoneType             : Forward
AccessScopePath      : \Global\Dublin
IsSigned             : False
DynamicUpdateStatus  : None
ScavengeStaleRecords : False

PS C:\Users\Administrator.CONTOSO> $a = Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com
PS C:\Users\Administrator.CONTOSO> Set-IpamAccessScope -IpamDnsZone -InputObject $a -AccessScopePath \Global\Europe -PassThru

ZoneName             : dublin.contoso.com
ZoneType             : Forward
AccessScopePath      : \Global\Europe
IsSigned             : False
DynamicUpdateStatus  : None
ScavengeStaleRecords : False
```
