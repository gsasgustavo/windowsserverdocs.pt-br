---
title: makecab
description: Artigo de referência para o comando Makecab, que empacota arquivos existentes em um arquivo de gabinete (. cab).
ms.topic: reference
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 560a2a75c756fb90b87da9f63a86a6dc887f836b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023680"
---
# <a name="makecab"></a>makecab

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Empacotar arquivos existentes em um arquivo de gabinete (. cab).


> [!NOTE]
> Esse comando é o mesmo que o [comando diantz](diantz.md).

## <a name="syntax"></a>Sintaxe

```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<source>` | Arquivo a ser compactado. |
| `<destination>` | Nome do arquivo para fornecer o arquivo compactado. Se omitido, o último caractere do nome do arquivo de origem será substituído por um sublinhado (_) e usado como o destino. |
| /f `<directives_file>` | Um arquivo com diretivas **Makecab** (pode ser repetido). |
| /d var =`<value>` | Define a variável com o valor especificado. |
| /l `<dir>` | Local para colocação de destino (o padrão é o diretório atual). |
| /v [ `<n>` ] | Definir nível de detalhamento de depuração (0 = nenhum,..., 3 = completo). |
| /? | Exibe a ajuda no prompt de comando. |

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando diantz](diantz.md)

- [Formato de gabinete da Microsoft](/previous-versions/bb417343(v=msdn.10))
