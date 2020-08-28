---
title: ksetup domain
description: Artigo de referência para o comando de domínio ksetup, que define o nome de domínio para todas as operações Kerberos.
ms.topic: reference
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9e89023e127318139672581cbab267a34c67a58
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025530"
---
# <a name="ksetup-domain"></a>ksetup domain

Define o nome de domínio para todas as operações Kerberos.

## <a name="syntax"></a>Sintaxe

```
ksetup /domain <domainname>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<domainname>` | Nome do domínio ao qual você deseja estabelecer uma conexão. Use o nome de domínio totalmente qualificado ou uma forma simples do nome, como contoso.com ou contoso.|

### <a name="examples"></a>Exemplos

Para estabelecer uma conexão com um domínio válido, como a Microsoft, usando o `ksetup /mapuser` subcomando, digite:

```
ksetup /mapuser principal@realm domain-user /domain domain-name
```

Após uma conexão bem-sucedida, você receberá uma nova TGT ou um TGT existente será atualizado.

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando ksetup](ksetup.md)

- [comando ksetup mapuser](ksetup-mapuser.md)