---
title: tipo
description: Artigo de referência para o comando Type, que exibe o conteúdo de um arquivo de texto.
ms.topic: reference
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2020
ms.openlocfilehash: 911a7bc36f3aa4cc1be9dbbcba58432abed9bb14
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947292"
---
# <a name="type"></a>tipo

No Shell de comando do Windows, **tipo** é um comando interno que exibe o conteúdo de um arquivo de texto. Use o comando **Type** para exibir um arquivo de texto sem modificá-lo.

No PowerShell, **Type** é um alias interno para o [cmdlet Get-Content](/powershell/module/microsoft.powershell.management/get-content), que também exibe o conteúdo de um arquivo, mas usando uma sintaxe diferente.

## <a name="syntax"></a>Sintaxe

```
type [<drive>:][<path>]<filename>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| `[<drive>:][<path>]<filename>` | Especifica o local e o nome do arquivo ou arquivos que você deseja exibir. Se o `<filename>` contiver espaços, você deverá colocá-lo entre aspas (por exemplo, "nome de arquivo contendo Spaces.txt"). Você também pode adicionar vários nomes de FileName adicionando espaços entre eles. |
| /? | Exibe a ajuda no prompt de comando. |

#### <a name="remarks"></a>Comentários

- Se você exibir um arquivo binário ou um arquivo criado por um programa, poderá ver caracteres estranhos na tela, incluindo caracteres formfeed e símbolos de sequência de escape. Esses caracteres representam códigos de controle que são usados no arquivo binário. Em geral, evite usar o comando **Type** para exibir arquivos binários.

## <a name="examples"></a>Exemplos

Para exibir o conteúdo de um arquivo chamado *feriado. mar*, digite:

```
type holiday.mar
```

Para exibir o conteúdo de um arquivo demorado chamado *feriado. mar* uma tela por vez, digite:

```
type holiday.mar | more
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
