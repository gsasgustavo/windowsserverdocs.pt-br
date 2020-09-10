---
title: bitsadmin setclientcertificatebyname
description: Artigo de referência para o comando Bitsadmin setclientcertificatebyname, que especifica o nome da entidade do certificado do cliente a ser usado para autenticação de cliente em uma solicitação HTTPS (SSL).
ms.topic: reference
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f5a29448641d7d92594e229396146169c3f6a9f4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631046"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bitsadmin setclientcertificatebyname

Especifica o nome do assunto do certificado do cliente a ser usado para autenticação de cliente em uma solicitação HTTPS (SSL).

## <a name="syntax"></a>Sintaxe

```
bitsadmin /setclientcertificatebyname <job> <store_location> <store_name> <subject_name>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| -------------- | -------------- |
| trabalho | O nome de exibição ou o GUID do trabalho. |
| store_location | Identifica o local de um armazenamento do sistema a ser usado para pesquisar o certificado. Os valores possíveis incluem:<ul><li>1 (CURRENT_USER)</li><li>2 (LOCAL_MACHINE)</li><li>3 (CURRENT_SERVICE)</li><li>4 (SERVIÇOS)</li><li>5 (USUÁRIOS)</li><li>6 (CURRENT_USER_GROUP_POLICY)</li><li>7 (LOCAL_MACHINE_GROUP_POLICY)</li><li>8 (LOCAL_MACHINE_ENTERPRISE)</li></ul> |
| store_name | O nome do repositório de certificados. Os valores possíveis incluem:<ul><li>AC (certificados de autoridade de certificação)</li><li>MEU (certificados pessoais)</li><li>RAIZ (certificados raiz)</li><li>SPC (certificado do fornecedor de software)</li></ul> |
| subject_name | Nome do certificado. |

## <a name="examples"></a>Exemplos

Para especificar o nome do certificado de cliente *myCertificate* a ser usado para autenticação de cliente em uma solicitação HTTPS (SSL) para o trabalho chamado *myDownloadJob*:

```
bitsadmin /setclientcertificatebyname myDownloadJob 1 MY myCertificate
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Bitsadmin](bitsadmin.md)
