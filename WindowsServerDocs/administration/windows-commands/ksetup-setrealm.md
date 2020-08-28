---
title: ksetup setrealm
description: Artigo de referência para o comando ksetup setrealm, que define o nome de um realm Kerberos.
ms.topic: reference
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53de8c94e20f496a6f3078d3ad03a817f23e326a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025360"
---
# <a name="ksetup-setrealm"></a>ksetup setrealm

Define o nome de um realm Kerberos.

> [!IMPORTANT]
> Não há suporte para a definição do realm Kerberos em um controlador de domínio. A tentativa de fazer isso causa um aviso e uma falha de comando.

## <a name="syntax"></a>Sintaxe

```
ksetup /setrealm <DNSdomainname>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<DNSdomainname>` | Especifica o nome DNS em maiúsculas, como CORP. CONTOSO.COM. Você pode usar o nome de domínio totalmente qualificado ou uma forma simples do nome. Se você não usar letras maiúsculas para o nome DNS, será solicitado que você faça a verificação para continuar. |

### <a name="examples"></a>Exemplos

Para definir o realm deste computador para um nome de domínio específico e para restringir o acesso por um controlador que não seja de domínio apenas ao realm Kerberos do CONTOSO, digite:

```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando ksetup](ksetup.md)

- [ksetup removerealm](ksetup-removerealm.md)
