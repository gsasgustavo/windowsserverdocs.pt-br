---
title: ftp get
description: Artigo de referência para o comando Get do FTP, que copia um arquivo remoto para o computador local usando o tipo de transferência de arquivo atual.
ms.topic: reference
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55e57167b7918aee7db9fc8f6f9304273dfcc4e0
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037734"
---
# <a name="ftp-get"></a>ftp get

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Copia um arquivo remoto para o computador local usando o tipo de transferência de arquivo atual.

> [!NOTE]
> Esse comando é o mesmo que o [comando de recebimento de FTP](ftp-recv.md).

## <a name="syntax"></a>Sintaxe

```
get <remotefile> [<localfile>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<remotefile>` | Especifica o arquivo remoto a ser copiado. |
| `[<localfile>]` | Especifica o nome do arquivo a ser usado no computador local. Se *LocalFile* não for especificado, o arquivo receberá o nome do *remotefile*. |

### <a name="examples"></a>Exemplos

Para copiar *test.txt* para o computador local usando a transferência de arquivo atual, digite:

```
get test.txt
```

Para copiar *test.txt* para o computador local como *test1.txt* usando a transferência de arquivo atual, digite:

```
get test.txt test1.txt
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando de recebimento de FTP](ftp-recv.md)

- [comando FTP ASCII](ftp-ascii.md)

- [comando Binary FTP](ftp-binary.md)

- [Diretrizes adicionais de FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
