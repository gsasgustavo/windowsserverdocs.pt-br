---
title: cache Bitsadmin e deleteURL
description: Artigo de referência para o cache Bitsadmin e o comando deleteURL, que exclui todas as entradas de cache para a URL fornecida.
ms.topic: reference
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed804580c4435b612b91875ef59cf6eb8ca4275b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026704"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>cache Bitsadmin e deleteURL

Exclui todas as entradas de cache para a URL fornecida.

## <a name="syntax"></a>Sintaxe

```
bitsadmin /deleteURL URL
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| -------------- | -------------- |
| URL | O localizador de recursos uniforme que identifica um arquivo remoto. |

## <a name="examples"></a>Exemplos

Para excluir todas as entradas de cache para `https://www.contoso.com/en/us/default.aspx` :

```
bitsadmin /deleteURL https://www.contoso.com/en/us/default.aspx
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando de cache Bitsadmin](bitsadmin-cache.md)
