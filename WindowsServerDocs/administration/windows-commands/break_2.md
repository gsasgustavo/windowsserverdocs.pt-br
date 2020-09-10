---
title: interrupção (volume da cópia de sombra)
description: Artigo de referência para o comando break, que Desassocia um volume de cópia de sombra do VSS e o torna acessível como um volume regular.
ms.topic: reference
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fa698a91ec7ddcabba7bcaaa6a80dac0831312af
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630037"
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