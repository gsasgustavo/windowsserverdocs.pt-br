---
title: Remove-DriverGroupFilter
description: Artigo de referência para Remove-DriverGroupFilter, que remove uma regra de filtro de um grupo de drivers em um servidor.
ms.topic: reference
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ed154b0ef50ebf36b716ad93d30768739b39ffb5
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91729612"
---
# <a name="remove-drivergroupfilter"></a>Remove-DriverGroupFilter



Remove uma regra de filtro de um grupo de drivers em um servidor.

## <a name="syntax"></a>Sintaxe

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------|-----------|
|/DriverGroup:\<Group Name>|Especifica o nome do grupo de drivers.|
|[/Server:\<Server name>]|Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN. Se um nome de servidor não for especificado, o servidor local será usado.|
|[/FilterType: \<FilterType> ]|Especifica o tipo do filtro a ser removido do grupo. \<FilterType> pode ser um dos seguintes:</br>**BiosVendor**</br>**Biosversion**</br>**ChassisType**</br>**Manufacturer**</br>**Personalizado**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**|

## <a name="examples"></a>Exemplos

Para remover um filtro, digite um dos seguintes:
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)