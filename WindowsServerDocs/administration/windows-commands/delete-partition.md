---
title: delete partition
description: Artigo de referência do comando Excluir partição, que exclui a partição com foco.
ms.topic: reference
ms.assetid: 65752312-cb16-46f6-870f-1b95c507b101
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2833039c9237a271910c43ff8acb7b8fb94828f1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628836"
---
# <a name="delete-partition"></a>delete partition

Exclui a partição com foco. Antes de começar, você deve selecionar uma partição para que essa operação seja realizada com sucesso. Use o comando [selecionar partição](select-partition.md) para selecionar uma partição e deslocar o foco para ela.

> [!WARNING]
> A exclusão de uma partição em um disco dinâmico pode excluir todos os volumes dinâmicos no disco, destruindo todos os dados e deixando o disco em um estado corrompido.
>
> Não é possível excluir a partição do sistema, a partição de inicialização ou qualquer partição que contenha o arquivo de paginação ativo ou informações de despejo de memória.

## <a name="syntax"></a>Sintaxe

```
delete partition [noerr] [override]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| NOERR | Somente para scripts. Quando um erro é encontrado, o DiskPart continua processando comandos como se o erro não tivesse ocorrido. Sem esse parâmetro, um erro faz com que o DiskPart saia com um código de erro. |
| override | Permite que o DiskPart exclua qualquer partição, independentemente do tipo. Normalmente, o DiskPart só permite que você exclua partições de dados conhecidas. |

#### <a name="remarks"></a>Comentários

- Para excluir um volume dinâmico, sempre use o comando [delete volume](delete-volume.md) .

- As partições podem ser excluídas de discos dinâmicos, mas não devem ser criadas. Por exemplo, é possível excluir uma partição GPT (tabela de partição GUID) não reconhecida em um disco GPT dinâmico. A exclusão dessa partição não faz com que o espaço livre resultante fique disponível. Em vez disso, esse comando destina-se a permitir que você recupere espaço em um disco dinâmico offline corrompido em uma situação de emergência em que o comando [Clean](clean.md) no DiskPart não possa ser usado.

## <a name="examples"></a>Exemplos

Para excluir a partição com foco, digite:

```
delete partition
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [select partition](select-partition.md)

- [Excluir comando](delete.md)

- [comando excluir volume](delete-volume.md)

- [Limpar comando](clean.md)
