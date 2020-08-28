---
title: bitsadmin setsecurityflags
description: Artigo de referência para o comando Bitsadmin setsecurityflags, que define sinalizadores de segurança para HTTP para determinar se o BITS deve verificar a lista de certificados revogados, ignorar determinados erros de certificado e definir a política a ser usada quando um servidor redireciona a solicitação HTTP.
ms.topic: reference
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 56f1888eef89a0d6ef6dbe70ea08e99503e0d8b6
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034734"
---
# <a name="bitsadmin-setsecurityflags"></a>bitsadmin setsecurityflags

Define sinalizadores de segurança para HTTP para determinar se o BITS deve verificar a lista de certificados revogados, ignorar determinados erros de certificado e definir a política a ser usada quando um servidor redireciona a solicitação HTTP. O valor é um inteiro sem sinal.

## <a name="syntax"></a>Sintaxe

```
bitsadmin /setsecurityflags <job> <value>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| -------------- | -------------- |
| trabalho | O nome de exibição ou o GUID do trabalho. |
| value | Pode incluir um ou mais dos seguintes sinalizadores de notificação, incluindo:<ul><li>Defina o bit menos significativo para habilitar a verificação de CRL.</li><li>Defina o 2º bit da direita para ignorar nomes comuns incorretos no certificado do servidor.</li><li>Defina o terceiro bit da direita para ignorar as datas incorretas no certificado do servidor.</li><li>Defina o 4º bit da direita para ignorar autoridades de certificação incorretas no certificado do servidor.</li><li>Defina o quinto bit da direita para ignorar o uso incorreto do certificado do servidor.</li><li>Defina o nono através dos bits 11 do lado direito para implementar sua política de redirecionamento especificada, incluindo:<ul><li>**0, 0, 0.** Os redirecionamentos são permitidos automaticamente.</li><li>**0, 0, 1.** O nome remoto na interface **IBackgroundCopyFile** será atualizado se ocorrer um redirecionamento.</li><li>**0, 1, 0.** O BITS falhará no trabalho se ocorrer um redirecionamento.</li></ul></li><li>Defina o 12 bits à direita para permitir o redirecionamento de HTTPS para HTTP.</li></ul> |

## <a name="examples"></a>Exemplos

Para definir os sinalizadores de segurança para habilitar uma verificação de CRL para o trabalho chamado *myDownloadJob*:

```
bitsadmin /setsecurityflags myDownloadJob 0x0001
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Bitsadmin](bitsadmin.md)
