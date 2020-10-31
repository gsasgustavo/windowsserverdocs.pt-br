---
title: WDSUTIL Enable-TransportServer
description: Artigo de referência para o comando WDSUTIL Enable-TransportServer, que habilita todos os serviços do servidor de transporte.
ms.topic: reference
ms.assetid: 9d79dba1-4b57-4a00-8cba-877e6b8618e6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b698a9fae2d730a78497fffe52dc91a68175f0f3
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070298"
---
# <a name="wdsutil-enable-transportserver"></a>WDSUTIL Enable-TransportServer

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Habilita todos os serviços para o servidor de transporte.

## <a name="syntax"></a>Sintaxe

```
wdsutil [options] /Enable-TransportServer [/Server:<Servername>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| [/Server:`<Servername>`] | Especifica o nome do servidor. Esse pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado. |

## <a name="examples"></a>Exemplos

Para habilitar os serviços no servidor, digite:

```
wdsutil /Enable-TransportServer
```

```
wdsutil /verbose /Enable-TransportServer /Server:MyWDSServer
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando WDSUTIL Disable-TransportServer](wdsutil-disable-transportserver.md)

- [comando WDSUTIL Get-TransportServer](wdsutil-get-transportserver.md)

- [comando WDSUTIL Set-TransportServer](wdsutil-set-transportserver.md)

- [comando WDSUTIL Start-TransportServer](wdsutil-start-transportserver.md)

- [comando WDSUTIL Stop-TransportServer](wdsutil-stop-transportserver.md)

- [Cmdlets dos serviços de implantação do Windows](/powershell/module/wds)
