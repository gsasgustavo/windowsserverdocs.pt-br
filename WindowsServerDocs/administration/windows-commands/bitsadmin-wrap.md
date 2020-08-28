---
title: bitsadmin wrap
description: Artigo de referência para o comando Bitsadmin Wrap, que encapsula qualquer linha de texto de saída que se estende além da borda mais à direita da janela de comando para a próxima linha.
ms.topic: reference
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 14ea78a09af0ba4dedce8438c5ec80cc39fcec9a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034634"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Encapsula qualquer linha de texto de saída que se estenda além da borda mais à direita da janela de comando para a próxima linha. Você deve especificar essa opção antes de qualquer outra opção.

Por padrão, todas as opções, exceto a opção de [Monitor Bitsadmin](bitsadmin-monitor.md) , encapsulam o texto de saída.

## <a name="syntax"></a>Sintaxe

```
bitsadmin /wrap <job>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ---------- |
| trabalho | O nome de exibição ou o GUID do trabalho. |

## <a name="examples"></a>Exemplos

Para recuperar informações para o trabalho chamado *myDownloadJob* e encapsular o texto de saída:

```
bitsadmin /wrap /info myDownloadJob /verbose
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Bitsadmin](bitsadmin.md)
