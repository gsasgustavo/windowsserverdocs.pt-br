---
title: WDSUTIL Get-alldrivergroups
description: Artigo de referência do comando WDSUTIL Get-alldrivergroups, que exibe informações sobre todos os grupos de drivers em um servidor.
ms.topic: reference
ms.assetid: f245ba53-f150-41b1-8418-38dcf0410a05
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b6d407e91af9132d6d2bc87ccb86320e3fe42b76
ms.sourcegitcommit: 28b5ab74cb0b40539ccc1a83998d6391e87fe51f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96614938"
---
# <a name="wdsutil-get-alldrivergroups"></a>WDSUTIL Get-alldrivergroups

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exibe informações sobre todos os grupos de drivers em um servidor.

## <a name="syntax"></a>Sintaxe

```
wdsutil /get-alldrivergroups [/server:<servername>] [/show:{packagemetadata | filters | all}]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| `[/server:<servername>]` | Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN. Se um nome de servidor não for especificado, o servidor local será usado. |
| `/show:{packagemetadata | filters | all}]` | Exibe os metadados de todos os pacotes de driver no grupo especificado. **PackageMetaData** exibe informações sobre todos os filtros para o grupo de drivers. **Filtros** exibe os metadados de todos os pacotes de driver e filtros para o grupo. |

## <a name="examples"></a>Exemplos

Para exibir informações sobre um arquivo de driver, digite:

```
wdsutil /get-alldrivergroups /server:MyWdsServer /show:All
```

```
wdsutil /get-alldrivergroups [/show:packagemetadata]
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
-
- [comando WDSUTIL Get-driver](wdsutil-get-drivergroup.md)
