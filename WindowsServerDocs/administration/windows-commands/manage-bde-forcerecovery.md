---
title: Manage-bde forcerecovery
description: Artigo de referência para o comando Manage-bde forcerecovery, que força uma unidade protegida pelo BitLocker para o modo de recuperação na reinicialização.
ms.topic: reference
ms.assetid: eecae37c-c9a3-46c5-b615-a0ace1f1d778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11dd4754ffebbd204e7ad463c56bce47f2a15714
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037684"
---
# <a name="manage-bde-forcerecovery"></a>Manage-bde forcerecovery

Força uma unidade protegida pelo BitLocker no modo de recuperação na reinicialização. Esse comando exclui todos os protetores de chave relacionados ao Trusted Platform Module (TPM) da unidade. Quando o computador é reiniciado, apenas uma senha de recuperação ou chave de recuperação pode ser usada para desbloquear a unidade.

## <a name="syntax"></a>Sintaxe

```
manage-bde –forcerecovery <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
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

Para fazer com que o BitLocker inicie no modo de recuperação na unidade C, digite:

```
manage-bde –forcerecovery C:
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Manage-bde](manage-bde.md)
