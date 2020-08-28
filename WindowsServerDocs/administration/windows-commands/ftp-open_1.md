---
title: ftp open
description: Artigo de referência para o comando FTP Open, que se conecta ao servidor FTP especificado.
ms.topic: reference
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a7599eb4728a46655b4c3274a9d7708061c3a9ee
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032814"
---
# <a name="ftp-open"></a>ftp open

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Conecta-se ao servidor FTP especificado.

## <a name="syntax"></a>Sintaxe

```
open <computer> [<port>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<computer>` | Especifica o computador remoto ao qual você está tentando se conectar. Você pode usar um endereço IP ou nome do computador (nesse caso, um servidor DNS ou um arquivo hosts deve estar disponível). |
| `[<port>]` | Especifica um número de porta TCP a ser usado para se conectar a um servidor FTP. Por padrão, a porta TCP 21 é usada. |

### <a name="examples"></a>Exemplos

Para se conectar ao servidor FTP em *ftp.Microsoft.com*, digite:

```
open ftp.microsoft.com
```

Para se conectar ao servidor FTP em *ftp.Microsoft.com* que está escutando na porta TCP *755*, digite:

```
open ftp.microsoft.com 755
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [Diretrizes adicionais de FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
