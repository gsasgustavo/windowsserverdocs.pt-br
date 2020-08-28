---
title: bitsadmin setcustomheaders
description: Artigo de referência para o comando Bitsadmin setcustomheaders, que adiciona um cabeçalho HTTP personalizado a uma solicitação GET.
ms.topic: reference
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84622cba8bb2bcb6a9ebfe782fdadc33a388fdb2
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031274"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

Adicione um cabeçalho HTTP personalizado a uma solicitação GET enviada a um servidor HTTP. Para obter mais informações sobre solicitações GET, consulte [definições de método](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) e definições de campo de [cabeçalho](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

## <a name="syntax"></a>Sintaxe

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| trabalho | O nome de exibição ou o GUID do trabalho. |
| `<header1> <header2>` e assim por diante | Os cabeçalhos personalizados para o trabalho. |

## <a name="examples"></a>Exemplos

Para adicionar um cabeçalho HTTP personalizado para o trabalho chamado *myDownloadJob*:

```
bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Bitsadmin](bitsadmin.md)
