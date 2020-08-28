---
title: gerenciar – retomar o BDE
description: Artigo de referência para o comando de retomada Manage-bde, que retoma a criptografia ou descriptografia do BitLocker depois que ele é pausado.
ms.topic: reference
ms.assetid: ca3cd1ca-6f2c-4190-b68f-27816635facb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 57f12ad478e565fa8edbeed0818e83b62c2d17fb
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027494"
---
# <a name="manage-bde-resume"></a>gerenciar – retomar o BDE

Retoma a criptografia ou descriptografia do BitLocker após sua pausa.

## <a name="syntax"></a>Sintaxe

```
manage-bde -resume [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<drive>` | Representa uma letra de unidade seguida de dois-pontos. |
| -ComputerName | Especifica que manage-bde.exe será usado para modificar a proteção do BitLocker em um computador diferente. Você também pode usar **-CN** como uma versão abreviada desse comando. |
| `<name>` | Representa o nome do computador no qual a proteção do BitLocker será modificada. Os valores aceitos incluem o nome NetBIOS do computador e o endereço IP do computador. |
| -? ou/? | Exibe a ajuda resumida no prompt de comando. |
| -Help ou-h | Exibe a ajuda completa no prompt de comando. |

### <a name="examples"></a>Exemplos

Para retomar a criptografia BitLocker na unidade C, digite:

```
manage-bde –resume C:
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [Manage-bde no comando](manage-bde-on.md)

- [comando Manage-bde off](manage-bde-off.md)

- [comando de pausa Manage-bde](manage-bde-pause.md)

- [comando Manage-bde](manage-bde.md)
