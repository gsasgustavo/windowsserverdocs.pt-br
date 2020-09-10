---
title: ksetup addenctypeattr
description: Artigo de referência para o comando ksetup addenctypeattr, que adiciona o atributo de tipo de criptografia à lista de tipos possíveis para o domínio.
ms.topic: reference
ms.assetid: 32cc87d7-b9e1-4d14-9eb7-3b439c55aa3a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ad11ed42a7a062a8c40d333055f2544a196b42a7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639763"
---
# <a name="ksetup-addenctypeattr"></a>ksetup addenctypeattr

Adiciona o atributo de tipo de criptografia à lista de tipos possíveis para o domínio. Uma mensagem de status é exibida após A conclusão bem-sucedida ou falha.

## <a name="syntax"></a>Sintaxe

```
ksetup /addenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<domainname>` | Nome do domínio ao qual você deseja estabelecer uma conexão. Use o nome de domínio totalmente qualificado ou uma forma simples do nome, como corp.contoso.com ou contoso. |
| tipo de criptografia | Deve ser um dos seguintes tipos de criptografia com suporte:<ul><li>DES-CBC-CRC</li><li>DES-CBC-MD5</li><li>RC4-HMAC-MD5</li><li>AES128-CTS-HMAC-SHA1-96</li><li>AES256-CTS-HMAC-SHA1-96</li></ul> |

#### <a name="remarks"></a>Comentários

- Você pode definir ou adicionar vários tipos de criptografia separando os tipos de criptografia no comando com um espaço. No entanto, você só pode fazer isso para um domínio de cada vez.

### <a name="examples"></a>Exemplos

Para exibir o tipo de criptografia para o tíquete de concessão de tíquete (TGT) e a chave de sessão do Kerberos, digite:

```
klist
```

Para definir o domínio como corp.contoso.com, digite:

```
ksetup /domain corp.contoso.com
```

Para adicionar o tipo de criptografia *AES-256-CTS-HMAC-SHA1-96* à lista de tipos possíveis para o domínio *Corp.contoso.com*, digite:

```
ksetup /addenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

Para definir o atributo de tipo de criptografia como *AES-256-CTS-HMAC-SHA1-96* para o domínio *Corp.contoso.com*, digite:

```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

Para verificar se o atributo de tipo de criptografia foi definido como pretendido para o domínio, digite:

```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando klist](klist.md)

- [comando ksetup](ksetup.md)

- [comando de domínio ksetup](ksetup-domain.md)

- [comando ksetup setenctypeattr](ksetup-setenctypeattr.md)

- [comando ksetup getenctypeattr](ksetup-getenctypeattr.md)

- [comando ksetup delenctypeattr](ksetup-delenctypeattr.md)
