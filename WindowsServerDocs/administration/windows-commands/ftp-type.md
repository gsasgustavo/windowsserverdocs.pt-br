---
title: ftp type
description: Artigo de referência para o comando de tipo FTP, que define ou exibe o tipo de transferência de arquivo.
ms.topic: reference
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f97c7959fcc0788298055b989433eec572d61584
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035684"
---
# <a name="ftp-type"></a>ftp type

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Define ou exibe o tipo de transferência de arquivo. O comando **FTP** dá suporte aos tipos de transferência de arquivo ASCII (padrão) e de imagem binária:

- É recomendável usar ASCII ao transferir arquivos de texto. No modo ASCII, conversões de caracteres de e para o conjunto de caracteres padrão de rede são executadas. Por exemplo, caracteres de fim de linha são convertidos conforme necessário, com base no sistema operacional de destino.

- É recomendável usar Binary ao transferir arquivos executáveis. No modo binário, os arquivos são transferidos em unidades de um byte.

## <a name="syntax"></a>Sintaxe

```
type [<typename>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `[<typename>]` | Especifica o tipo de transferência de arquivo. Se você não especificar esse parâmetro, o tipo atual será exibido.|

### <a name="examples"></a>Exemplos

Para definir o tipo de transferência de arquivo como ASCII, digite:

```
type ascii
```

Para definir o tipo de arquivo de transferência como binário, digite:

```
type binary
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [Diretrizes adicionais de FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
