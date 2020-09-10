---
title: bitsadmin sethelpertokenflags
description: Artigo de referência para o comando Bitsadmin sethelpertokenflags, que define os sinalizadores de uso para um token auxiliar que está associado a um trabalho de transferência de BITS.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 23a2626fcd1eb92c388ea1dc24682526bac59af5
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630883"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

Define os sinalizadores de uso para um [token auxiliar](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)   que está associado a um trabalho de transferência de bits.

> [!NOTE]
> Esse comando não tem suporte no BITS 3,0 e versões anteriores.

## <a name="syntax"></a>Sintaxe

```
bitsadmin /sethelpertokenflags <job> <flags>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| trabalho | O nome de exibição ou o GUID do trabalho. |
| sinalizadores | Possíveis valores de token auxiliares, incluindo:<ul><li>**0x0001.** Usado para abrir o arquivo local de um trabalho de carregamento, para criar ou renomear o arquivo temporário de um trabalho de download, ou para criar ou renomear o arquivo de resposta de um trabalho de resposta de upload.</li><li>**0x0002.** Usado para abrir o arquivo remoto de um upload ou um trabalho de download do protocolo SMB ou em resposta a um servidor HTTP ou a um desafio de proxy para credenciais NTLM ou Kerberos implícitas.</li></ul>Você deve chamar  `/setcredentialsjob targetscheme null null`   para enviar as credenciais por http. |

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Bitsadmin](bitsadmin.md)
