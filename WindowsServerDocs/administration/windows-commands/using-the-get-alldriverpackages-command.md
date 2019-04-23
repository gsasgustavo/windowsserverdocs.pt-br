---
title: Usando o comando get-AllDriverPackages
description: 'Tópico de comandos do Windows para * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9eb8fcb7-ef46-4c8d-9623-8969a3c8b8a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e531d9e175ba35aa092c1ef95ec5fe7d1eddff6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843647"
---
# <a name="using-the-get-alldriverpackages-command"></a>Usando o comando get-AllDriverPackages

>Aplica-se a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exibe informações sobre todos os pacotes de driver em um servidor que correspondem aos critérios de pesquisa especificados.
## <a name="syntax"></a>Sintaxe
```
wdsutil /Get-AllDriverPackages [/Server:<Server name>] [/Show:{Drivers | Files | All}] [/Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]]
```
## <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
|[/Server:<Server name>]|O nome do servidor. Isso pode ser o nome NetBIOS ou FQDN. Se não for especificado um nome de servidor, o servidor local será usado.|
|[/Show: {Drivers &#124; Files &#124; All}]|Indica as informações do pacote para exibir. Se **/Mostrar** não for especificado, o padrão é retornar somente o driver de metadados do pacote. **Drivers** exibe a lista de drivers no pacote. **Arquivos** exibe a lista de arquivos no pacote. **Todos os** exibe drivers e arquivos.|
|/Filtertype:<Filter type>|Especifica o atributo do pacote de driver a ser pesquisado. Você pode especificar vários atributos em um único comando. Você também deve especificar **/Operator** e **/valor** com essa opção.<br /><br /><Filter type> Pode ser uma das seguintes opções:<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/Operator:{Equal &#124; NotEqual &#124; GreaterOrEqual &#124; LessOrEqual &#124; Contains}|Especifica a relação entre o atributo e os valores. Você pode especificar **Contains** apenas com atributos de cadeia de caracteres. Você pode especificar **GreaterOrEqual** e **LessOrEqual** apenas com atributos de data e a versão.|
|/Value:<Value>|Especifica o valor de pesquisa especificado <attribute>.  Você pode especificar vários valores para uma única **/Filtertype**. A lista a seguir descreve os atributos que você pode especificar para cada filtro. Para obter mais informações sobre esses atributos, consulte [atributos de Driver e pacote](https://go.microsoft.com/fwlink/?LinkId=166895) (https://go.microsoft.com/fwlink/?LinkId=166895).<br /><br />-PackageId - especifique um GUID válido. Por exemplo: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-PackageName especificar qualquer valor de cadeia de caracteres.<br />-Especifique PackageEnabled - **Yes** ou **não**.<br />-Packagedateadded - especifique a data no seguinte formato: AAAA/MM/DD<br />-PackageInfFilename especificar qualquer valor de cadeia de caracteres.<br />-PackageClass - especifique um nome de classe válido ou o GUID de classe. Por exemplo: **Unidade de disco**, **Net**, ou {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-PackageProvider especificar qualquer valor de cadeia de caracteres.<br />-Especifique PackageArchitecture - **x86**, **x64**, ou **ia64**.<br />-PackagLocale - especifique um identificador de idioma válido. Por exemplo: **en-US** ou **es-ES**.<br />-Especifique PackageSigned - **Yes** ou **não**.<br />-PackagedatePublished - especifique a data no seguinte formato: AAAA/MM/DD<br />-Packageversion especifique a versão no seguinte formato: a.b.x.y. Por exemplo: 6.1.0.0<br />-Driverdescription especificar qualquer valor de cadeia de caracteres.<br />-DriverManufacturer especificar qualquer valor de cadeia de caracteres.<br />-DriverHardwareId - especificar qualquer valor de cadeia de caracteres.<br />-DrivercompatibleId - especificar qualquer valor de cadeia de caracteres.<br />-DriverExcludeId especificar qualquer valor de cadeia de caracteres.<br />-DriverGroupId especifique um GUID válido. Por exemplo: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-DriverGroupName especificar qualquer valor de cadeia de caracteres.|
## <a name="BKMK_examples"></a>Exemplos
Para exibir informações, digite um dos seguintes:
```
wdsutil /Get-AllDriverPackages /Server:MyWdsServer /Show:All /Filtertype:DriverGroupName /Operator:Contains /Value:printer /Filtertype:PackageArchitecture /Operator:Equal /Value:x64 /Value:x86
```
```
wdsutil /Get-AllDriverPackages /Show:Drivers /Filtertype:Packagedateadded /Operator:GreaterOrEqual /Value:2008/01/01
```
#### <a name="additional-references"></a>Referências adicionais
[Chave de sintaxe de linha de comando](command-line-syntax-key.md)
[usando o comando get-/InfFile](using-the-get-driverpackage-command.md)
[usando o comando get-DriverPackageFile](using-the-get-driverpackagefile-command.md)