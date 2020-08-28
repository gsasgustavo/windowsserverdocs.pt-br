---
title: select partition
description: Artigo de referência para * * * *-
ms.topic: reference
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 816a235f7ba83320828a5dc72c9f2558c27b2ed8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027904"
---
# <a name="select-partition"></a>select partition

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

seleciona a partição especificada e desloca o foco para ela. Esse comando também pode ser usado para exibir a partição que atualmente tem o foco no disco selecionado.



## <a name="syntax"></a>Sintaxe

```
select partition=<n>
```

### <a name="parameters"></a>Parâmetros

|   Parâmetro    |                                                                                    Descrição                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| particion\=<n> | O número da partição que receberá o foco. Você pode exibir os números de todas as partições no disco selecionado no momento usando o comando **listar partição** no DiskPart. |

## <a name="remarks"></a>Comentários

-   Para poder selecionar uma partição, primeiro você deve selecionar um disco usando o comando **selecionar disco** .

-   Se nenhum número de partição for especificado, esse comando exibirá a partição que atualmente tem o foco no disco selecionado.

-   se um volume for selecionado com uma partição correspondente, a partição será selecionada automaticamente.

-   se uma partição for selecionada com um volume correspondente, o volume será selecionado automaticamente.

## <a name="examples"></a>Exemplos
Para deslocar o foco para a partição 3, digite:

```
select partitition=3
```

Para exibir a partição que atualmente tem o foco no disco selecionado, digite:

```
select partition
```

## <a name="additional-references"></a>Referências adicionais
- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)




