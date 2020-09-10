---
title: popd
description: Artigo de referência para o comando pnputil, que altera o diretório atual para o diretório que foi armazenado mais recentemente pelo comando Pushed.
ms.topic: reference
ms.assetid: 8a4c52d5-9fd1-4eac-9c0c-5767b25728ed
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 4884e294f878a55125a035d7113ce857e1964634
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633651"
---
# <a name="popd"></a>popd

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

O comando **popd** altera o diretório atual para o diretório que foi armazenado mais recentemente pelo comando **Pushed** .

Sempre que você usa o comando **PUSHD** , um único diretório é armazenado para seu uso. No entanto, você pode armazenar vários diretórios usando o comando **PUSHD** várias vezes. Os diretórios são armazenados em sequência em uma pilha virtual, portanto, se você usar o comando **PUSHD** uma vez, o diretório no qual você usa o comando será colocado na parte inferior da pilha. Se você usar o comando novamente, o segundo diretório será colocado na parte superior do primeiro. O processo é repetido sempre que você usa o comando **PUSHD** .

Se você usar o comando **popd** , o diretório na parte superior da pilha será removido e o diretório atual será alterado para esse diretório. Se você usar o comando **popd** novamente, o próximo diretório na pilha será removido. Se as extensões de comando estiverem habilitadas, o comando **popd** removerá as atribuições de letra de unidade criadas pelo comando **PUSHD** .

## <a name="syntax"></a>Sintaxe

```
popd
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | DESCRIÇÃO |
|--|--|
| /? | Exibe a ajuda no prompt de comando. |

### <a name="examples"></a>Exemplos

Para alterar o diretório atual daquele em que o programa do lote foi executado e, em seguida, alterá-lo de volta, digite:

```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [pushd](pushd.md)
