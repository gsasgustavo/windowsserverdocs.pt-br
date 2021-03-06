---
title: dfsdiag testdfsintegrity
description: Artigo de referência para o comando Dfsdiag testdfsintegrity, que verifica a integridade do namespace do Sistema de Arquivos Distribuído (DFS).
ms.topic: reference
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4aa6eb44084ec939ebed708982e527b237d407c7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634150"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag testdfsintegrity

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verifica a integridade do namespace do Sistema de Arquivos Distribuído (DFS) executando os seguintes testes:

- Verifica se há danos ou inconsistências nos metadados do DFS entre os controladores de domínio.

- Valida a configuração da enumeração baseada em acesso para garantir que ela seja consistente entre os metadados do DFS e o compartilhamento do servidor de namespace.

- Detecta pastas DFS sobrepostas (links), pastas duplicadas e pastas com destinos de pasta sobrepostos.

## <a name="syntax"></a>Sintaxe

```
dfsdiag /testdfsintegrity /DFSroot: <DFS root path> [/recurse] [/full]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| /DFSroot: `<DFS root path>` | O namespace do DFS para diagnosticar. |
| /recurse | Executa o teste, incluindo qualquer Interlink de namespace. |
| /full | Verifica a consistência do compartilhamento e das ACLs de NTFS, juntamente com a configuração do lado do cliente em todos os destinos de pasta. Ele também verifica se a propriedade online está definida. |

## <a name="examples"></a>Exemplos

Para verificar a integridade e a consistência dos namespaces de Sistema de Arquivos Distribuído (DFS) no *contoso. com\MyNamespace*, incluindo quaisquer Interlinks, digite:

```
dfsdiag /testdfsintegrity /DFSRoot:\contoso.com\MyNamespace /recurse /full
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Dfsdiag](dfsdiag.md)
