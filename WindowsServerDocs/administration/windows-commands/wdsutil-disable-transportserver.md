---
title: WDSUTIL Disable-TransportServer
description: Artigo de referência para o comando WDSUTIL Disable-TransportServer, que desabilita todos os serviços de um servidor de transporte.
ms.topic: reference
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4bbb177897e3a779de275957949b0dcf62e53478
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070348"
---
# <a name="wdsutil-disable-transportserver"></a>WDSUTIL Disable-TransportServer

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Desabilita todos os serviços de um servidor de transporte.

## <a name="syntax"></a>Sintaxe

```
wdsutil [Options] /Disable-TransportServer [/Server:<Servername>]
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|-------|--------|
|[/Server:`<Servername>`]|Especifica o nome do servidor de transporte a ser desabilitado. Pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome do servidor de transporte for especificado, o servidor local será usado.|

## <a name="examples"></a>Exemplos

Para desabilitar o servidor, digite:

```
wdsutil /Disable-TransportServer
```

```
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando WDSUTIL Enable-TransportServer](wdsutil-enable-transportserver.md)

- [comando WDSUTIL Get-TransportServer](wdsutil-get-transportserver.md)

- [comando WDSUTIL Set-TransportServer](wdsutil-set-transportserver.md)

- [comando WDSUTIL Start-TransportServer](wdsutil-start-transportserver.md)

- [comando WDSUTIL Stop-TransportServer](wdsutil-stop-transportserver.md)

- [Cmdlets dos serviços de implantação do Windows](/powershell/module/wds)
