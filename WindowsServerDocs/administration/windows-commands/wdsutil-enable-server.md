---
title: WDSUTIL habilitar-servidor
description: Artigo de referência para o comando WDSUTIL Enable-Server, que habilita todos os serviços para os serviços de implantação do Windows.
ms.topic: reference
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e2f62198ce4c012245174bc00e536e15ecd1c27
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070318"
---
# <a name="wdsutil-enable-server"></a>WDSUTIL habilitar-servidor

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Habilita todos os serviços para serviços de implantação do Windows.

## <a name="syntax"></a>Sintaxe

```
wdsutil [options] /Enable-Server [/Server:<Servername>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| [/Server:`<Servername>`] | Especifica o nome do servidor. Esse pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado. |

## <a name="examples"></a>Exemplos

Para habilitar os serviços no servidor, digite:

```
wdsutil /Enable-Server
```

```
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [WDSUTIL Disable – comando do servidor](wdsutil-disable-server.md)

- [comando WDSUTIL Get-Server](wdsutil-get-server.md)

- [comando do servidor de inicialização WDSUTIL](wdsutil-initialize-server.md)

- [WDSUTIL Set-Server Command](wdsutil-set-server.md)

- [comando Start-Server do WDSUTIL](wdsutil-start-server.md)

- [comando WDSUTIL Stop-Server](wdsutil-stop-server.md)

- [WDSUTIL não inicializar-comando de servidor](wdsutil-uninitialize-server.md)

- [Cmdlets dos serviços de implantação do Windows](/powershell/module/wds)
