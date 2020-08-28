---
title: Remove-DriverPackage
description: Artigo de referência para Remove-DriverPackage, que remove um pacote de driver de um servidor.
ms.topic: reference
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5745b83fdb817f90a835fe2243aff21f9892be47
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023200"
---
# <a name="remove-driverpackage"></a>Remove-DriverPackage

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Remove um pacote de driver de um servidor.

## <a name="syntax"></a>Sintaxe
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>Parâmetros

|        Parâmetro        |                                                                            Descrição                                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |              Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN. Se um nome de servidor não for especificado, o servidor local será usado.              |
| [/DriverPackage: <Name> ] |                                                        Especifica o nome do pacote de driver a ser removido.                                                         |
|    [/PackageId: <ID> ]    | Especifica a ID dos serviços de implantação do Windows do pacote de driver a ser removido. Você deve especificar a ID se o pacote de driver não puder ser identificado exclusivamente pelo nome. |

## <a name="examples"></a>Exemplos
Para exibir informações sobre as imagens, digite um dos seguintes:
```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```
## <a name="additional-references"></a>Referências adicionais
- Chave de sintaxe [de linha de comando](command-line-syntax-key.md) 
 [Usando o comando Remove-DriverPackages](using-the-remove-driverpackages-command.md)
