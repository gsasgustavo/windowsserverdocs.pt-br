---
title: gerenciar – retomar o BDE
description: Artigo de referência para o comando de retomada Manage-bde, que retoma a criptografia ou descriptografia do BitLocker depois que ele é pausado.
ms.topic: reference
ms.assetid: ca3cd1ca-6f2c-4190-b68f-27816635facb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ebae22e60a8110bc2ba5e4649fc6cf143431b359
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639299"
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
