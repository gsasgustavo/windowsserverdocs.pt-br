---
title: mklink
description: Artigo de referência para o comando mklink, que cria um diretório ou arquivo de vínculo simbólico ou físico.
ms.topic: reference
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dd605283396757f1ef0de05d620583c895f71f1a
ms.sourcegitcommit: f18097c21e50a09aef2f1937f52608b0042ef0e1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96755303"
---
# <a name="mklink"></a>mklink

Cria um diretório ou arquivo de vínculo simbólico ou físico.

## <a name="syntax"></a>Sintaxe

```
mklink [[/d] | [/h] | [/j]] <link> <target>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| /d | Cria um link simbólico de diretório. Por padrão, esse comando cria um link simbólico de arquivo. |
| /h | Cria um link físico em vez de um link simbólico. |
| /j | Cria uma junção de diretório. |
| `<link>` | Especifica o nome do link simbólico que está sendo criado. |
| `<target>` | Especifica o caminho (relativo ou absoluto) ao qual o novo link simbólico se refere. |
| /? | Exibe a ajuda no prompt de comando. |

### <a name="examples"></a>Exemplos

Para criar e remover um link simbólico chamado MyFolder do diretório raiz para o diretório \Users\User1\Documents e um link físico chamado MyFile. File para o arquivo de exemplo. File localizado no diretório, digite:

```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando del](del.md)

- [comando RD](rd.md)

- [Novo item no Windows PowerShell](/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
