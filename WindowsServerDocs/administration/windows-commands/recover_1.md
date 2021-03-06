---
title: recuperar (DiskPart)
description: Artigo de referência do comando DiskPart Recover, que atualiza o estado de todos os discos em um grupo de discos, tenta recuperar discos em um grupo de discos inválido e ressincroniza volumes espelhados e volumes RAID-5 que têm dados obsoletos.
ms.topic: reference
ms.assetid: 8cc3a73d-9456-41a0-b375-2b4cc37c3992
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 55b31333f03ec90ba9c37b7d2e31c251893b18d8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637263"
---
# <a name="recover-diskpart"></a>recuperar (DiskPart)

Atualiza o estado de todos os discos em um grupo de discos, tenta recuperar discos em um grupo de discos inválido e sincroniza novamente os volumes espelhados e os volumes RAID-5 que têm dados obsoletos. Esse comando opera em discos que falharam ou falharam. Ele também opera em volumes que falharam, falham ou estão em estado de redundância com falha.

Esse comando opera em grupos de discos dinâmicos. Se esse comando for usado em um grupo com um disco básico, ele não retornará um erro, mas nenhuma ação será executada.

> [!NOTE]
> Um disco que faz parte de um grupo de discos deve ser selecionado para que essa operação seja realizada com sucesso. Use o [comando selecionar disco](select-disk.md) para selecionar um disco e deslocar o foco para ele.

## <a name="syntax"></a>Sintaxe

```
recover [noerr]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| NOERR | Somente para scripts. Quando um erro é encontrado, o DiskPart continua processando comandos como se o erro não tivesse ocorrido. Sem esse parâmetro, um erro faz com que o DiskPart saia com um código de erro. |

## <a name="examples"></a>Exemplos

Para recuperar o grupo de discos que contém o disco com foco, digite:

```
recover
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
