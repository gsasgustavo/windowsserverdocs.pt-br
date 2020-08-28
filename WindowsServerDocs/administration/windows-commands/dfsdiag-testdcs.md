---
title: dfsdiag testdcs
description: Artigo de referência para o comando Dfsdiag testdcs, que verifica a configuração de controladores de domínio no domínio especificado.
ms.topic: reference
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54bb3f2a1c724a77ab3a55c6f5158bda81de94f8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024020"
---
# <a name="dfsdiag-testdcs"></a>dfsdiag testdcs

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verifica a configuração de controladores de domínio executando os seguintes testes em cada controlador de domínio no domínio especificado:

- Verifica se o serviço de namespace do Sistema de Arquivos Distribuído (DFS) está em execução e se seu tipo de inicialização está definido como **automático**.

- Verifica o suporte de referências com custo de site para NETLOGON e SYSvol.

- Verifica a consistência da associação do site pelo nome do host e endereço IP.

## <a name="syntax"></a>Sintaxe

```
dfsdiag /testdcs [/domain:<domain_name>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| /Domain`<domain_name>` | Nome do domínio a ser verificado. Esse parâmetro é opcional. O valor padrão é o domínio local para o qual o host local está associado. |

## <a name="examples"></a>Exemplos

Para verificar a configuração dos controladores de domínio no domínio *contoso.com* , digite:

```
dfsdiag /testdcs /domain:contoso.com
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Dfsdiag](dfsdiag.md)
