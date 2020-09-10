---
title: bootcfg copy
description: Artigo de referência para o comando Bootcfg Copy, que faz uma cópia de uma entrada de inicialização existente, à qual você pode adicionar opções de linha de comando.
ms.topic: reference
ms.assetid: 2a236c2a-8675-444d-b695-9cbc9aff643b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 14d3a124c1c52b985ecff96da28e828f73abc1e3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630340"
---
# <a name="bootcfg-copy"></a>bootcfg copy

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Faz uma cópia de uma entrada de inicialização existente, à qual você pode adicionar opções de linha de comando.

## <a name="syntax"></a>Sintaxe

```
bootcfg /copy [/s <computer> [/u <domain>\<user> /p <password>]] [/d <description>] [/id <osentrylinenum>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `/s <computer>` | Especifica o nome ou o endereço IP de um computador remoto (não use barras invertidas). O padrão é o computador local. |
| `/u <domain>\<user>`  | Executa o comando com as permissões de conta do usuário especificado por `<user>` ou `<domain>\<user>` . O padrão é as permissões do usuário conectado no momento no computador que emite o comando. |
| `/p <password>` | Especifica a senha da conta de usuário que é especificada no parâmetro **/u** . |
| `/d <description>` | Especifica a descrição para a nova entrada do sistema operacional. |
| `/id <osentrylinenum>` | Especifica o número da linha de entrada do sistema operacional na seção [Operating Systems] do arquivo de Boot.ini ao qual as opções de carregamento do sistema operacional são adicionadas. A primeira linha após o cabeçalho da seção [Operating Systems] é 1. |
| /? | Exibe a ajuda no prompt de comando. |

## <a name="examples"></a>Exemplos

Para copiar a entrada de inicialização 1 e digite \ABC Server \ como a descrição:

```
bootcfg /copy /d \ABC Server\ /id 1
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Bootcfg](bootcfg.md)
