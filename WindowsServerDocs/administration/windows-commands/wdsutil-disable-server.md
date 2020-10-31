---
title: WDSUTIL Disable-Server
description: Artigo de referência para o comando WDSUTIL Disable-Server, que desabilita todos os serviços de um servidor de serviços de implantação do Windows.
ms.topic: reference
ms.assetid: b69fcfe0-b744-4794-bc75-2c9218c0ba66
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d8af0a0c929e2bff341b2b5bff71d0838b09d418
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070388"
---
# <a name="wdsutil-disable-server"></a>WDSUTIL Disable-Server

Desabilita todos os serviços de um servidor de serviços de implantação do Windows.

## <a name="syntax"></a>Sintaxe

```
wdsutil [Options] /Disable-Server [/Server:<Server name>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| [/Server:`<Servername>`] | Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado. |

## <a name="examples"></a>Exemplos

Para desabilitar o servidor, digite:

```
wdsutil /Disable-Server
```

```
wdsutil /Verbose /Disable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [Cmdlets dos serviços de implantação do Windows](/powershell/module/wds)
