---
title: desabilitar-TransportServer
description: Artigo de referência para Disable-TransportServer, que desabilita todos os serviços para um servidor de transporte.
ms.topic: reference
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2fd2ac1c346aca8132870edea2bf7696114089b2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622001"
---
# <a name="disable-transportserver"></a>desabilitar-TransportServer

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Desabilita todos os serviços de um servidor de transporte.

## <a name="syntax"></a>Sintaxe
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
|[/Server:<Server name>]|Especifica o nome do servidor de transporte a ser desabilitado. Pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome do servidor de transporte for especificado, o servidor local será usado.|
## <a name="examples"></a>Exemplos
Para desabilitar o servidor, digite:
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Referências adicionais
- Chave de sintaxe [de linha de comando](command-line-syntax-key.md) 
 [Usando o comando](using-the-enable-transportserver-command.md) 
 Enable-TransportServer [Usando o comando](using-the-get-transportserver-command.md) 
 Get-TransportServer [Subcomando: Set-TransportServer](subcommand-set-transportserver.md) 
 [Subcomando: Start-TransportServer](subcommand-start-transportserver.md) 
 [Subcomando: Stop-TransportServer](subcommand-stop-transportserver.md)
