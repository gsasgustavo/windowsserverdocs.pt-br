---
title: interrupção (volume da cópia de sombra)
description: Artigo de referência para o comando break, que Desassocia um volume de cópia de sombra do VSS e o torna acessível como um volume regular.
ms.topic: reference
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d94275b83ad65f70db4bd1850f55ea527292d1bc
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034304"
---
# <a name="break-shadow-copy-volume"></a>interrupção (volume da cópia de sombra)

Desassocia um volume de cópia de sombra do VSS e o torna acessível como um volume regular. O volume pode então ser acessado usando uma letra da unidade (se atribuída) ou o nome do volume. Se usado sem parâmetros, **Break** exibe a ajuda no prompt de comando.

> [!NOTE]
> Esse comando é relevante apenas para cópias de sombra de hardware após a importação.
>
> Os volumes expostos, como as cópias de sombra de origem, são somente leitura por padrão. O acesso ao volume é feito diretamente para o provedor de hardware sem registro do volume que tem sido uma cópia de sombra.

## <a name="syntax"></a>Sintaxe

```
break [writable] <setid>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| escrita | Habilita o acesso de leitura/gravação no volume. |
| \<setid> | Especifica a ID do conjunto de cópias de sombra. O alias da ID da cópia de sombra, que é armazenado como uma variável de ambiente pelo comando **carregar metadados** , pode ser usado no parâmetro *SetID* . |

## <a name="examples"></a>Exemplos

Para fazer uma cópia de sombra usando o nome do alias Alias1 acessível como um volume gravável no sistema operacional:

```
break writable %Alias1%
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)