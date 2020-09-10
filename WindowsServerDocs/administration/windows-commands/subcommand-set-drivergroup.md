---
title: Conjunto de subcomandos – grupo de drivers
description: Artigo de referência para subcomando set-Group-Driver, que define as propriedades de um grupo de drivers existente em um servidor.
ms.topic: reference
ms.assetid: e4ba9b1c-8c52-4fd5-969b-f7905611b364
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c4d014933ae4ebc530977325210887d4abf90817
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640901"
---
# <a name="subcommand-set-drivergroup"></a>Subcomando: Set-grupo de driver

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Define as propriedades de um grupo de drivers existente em um servidor.

## <a name="syntax"></a>Sintaxe
```
wdsutil /Set-DriverGroup /DriverGroup:<Group Name> [/Server:<Server Name>] [/Name:<New Group Name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}]
```
### <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
|/DriverGroup:<Group Name>|Especifica o nome do grupo de drivers.|
|[/Server:<Server name>]|Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN. Se um nome de servidor não for especificado, o servidor local será usado.|
|[/Name: <New Group Name> ]|Especifica o novo nome para o grupo de drivers.|
|[/Enabled: {Sim &#124; não}|Habilita ou desabilita o grupo de drivers.|
|[/Applicability: {Matchado &#124; All}]|Especifica quais pacotes instalar se os critérios de filtro forem atendidos. **MATCHED** significa instalar apenas os pacotes de driver que correspondem a um hardware de cliente. **Tudo** significa instalar todos os pacotes para clientes, independentemente de seu hardware.|
## <a name="examples"></a>Exemplos
Para definir as propriedades de um grupo de drivers, digite um dos seguintes:
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Name:colorprinterdrivers /Applicability:All
```
## <a name="additional-references"></a>Referências adicionais
- Chave de sintaxe [de linha de comando](command-line-syntax-key.md) 
 [Subcomando: Set-DriverGroupFilter](subcommand-set-drivergroupfilter.md)
