---
title: Usando o comando add-ImageDriverPackages
description: 'Tópico de comandos do Windows para * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9dc78909-a4d1-42a2-af8f-21ebcbfe8302
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55b26acf9c4006db3d64e27be8a10e158876ddc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817357"
---
# <a name="using-the-add-imagedriverpackages-command"></a>Usando o comando add-ImageDriverPackages

>Aplica-se a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

adiciona pacotes de driver do armazenamento do driver para uma imagem de inicialização. A versão da imagem deve ser Windows 7 ou Windows Server 2008 R2 ou posterior.
Para obter exemplos de como você pode usar esse comando, consulte [exemplos](#BKMK_examples).
## <a name="syntax"></a>Sintaxe
```
wdsutil /add-ImageDriverPackages [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64} 
[/Filename:<File name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]
```
## <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
|/Server:<Server name>|Especifica o nome do servidor. Isso pode ser o nome NetBIOS ou FQDN. Se nenhum nome de servidor for especificado, o servidor local será usado.|
mídia:<Image name>|Especifica o nome da imagem para adicionar o driver.|
mediatype:Boot|Especifica o tipo de imagem para adicionar o driver. Pacotes de driver podem ser adicionados apenas para imagens de inicialização.|
|/ Arquitetura: {x86 &#124; ia64 &#124; x64}|Especifica a arquitetura da imagem de inicialização. Como é possível ter o mesmo nome de imagem para imagens de inicialização em arquiteturas diferentes, você deve especificar a arquitetura para garantir que a imagem correta é usada.|
|/Filename:<File name>|Especifica o nome do arquivo. Se a imagem não pode ser identificada exclusivamente pelo nome, o nome do arquivo deve ser especificado.|
|/Filtertype:<Filter type>|Especifica o atributo do pacote de driver a ser pesquisado. Você pode especificar vários atributos em um único comando. Você também deve especificar **/Operator** e **/valor** com essa opção.<br /><br /><Filter type> Pode ser uma das seguintes opções:<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/Operator:{Equal &#124; NotEqual &#124; GreaterOrEqual &#124; LessOrEqual &#124; Contains}|A relação entre o atributo e os valores. Você só pode especificar **Contains** com atributos de cadeia de caracteres. Você só pode especificar **GreaterOrEqual** e **LessOrEqual** com atributos de data e a versão.|
|/Value:<Value>|Especifica o valor a ser pesquisado em relação ao especificado <attribute>. Você pode especificar vários valores para uma única **/Filtertype**. A lista a seguir mostra os atributos que você pode especificar para cada filtro. Para obter mais informações sobre esses atributos, consulte [atributos de Driver e pacote](https://go.microsoft.com/fwlink/?LinkId=166895) (https://go.microsoft.com/fwlink/?LinkId=166895).<br /><br />-PackageId - especifique um GUID válido. Por exemplo: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-PackageName especificar qualquer valor de cadeia de caracteres.<br />-Especifique PackageEnabled - **Yes** ou **não**.<br />-Packagedateadded - especifique a data no seguinte formato: AAAA/MM/DD<br />-PackageInfFilename especificar qualquer valor de cadeia de caracteres.<br />-PackageClass - especifique um nome de classe válido ou o GUID de classe. Por exemplo: **Unidade de disco**, **Net**, ou {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-PackageProvider especificar qualquer valor de cadeia de caracteres.<br />-Especifique PackageArchitecture - **x86**, **x64**, ou **ia64**.<b /> -PackageLocale - especifique um identificador de idioma válido. Por exemplo: **en-US** ou **es-ES**.<br />-Especifique PackageSigned - **Yes** ou **não**.<br />-PackagedatePublished - especifique a data no seguinte formato: AAAA/MM/DD<br />-Packageversion - especifique a versão no seguinte formato: a.b.x.y. Por exemplo:  6.1.0.0<br />-Driverdescription especificar qualquer valor de cadeia de caracteres.<br />-DriverManufacturer especificar qualquer valor de cadeia de caracteres.<br />-DriverHardwareId - especificar qualquer valor de cadeia de caracteres.<br />-DrivercompatibleId - especificar qualquer valor de cadeia de caracteres.<br />-DriverExcludeId - especificar qualquer valor de cadeia de caracteres.<br />-DriverGroupId - especifique um GUID válido. Por exemplo: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-DriverGroupName especificar qualquer valor de cadeia de caracteres.|
## <a name="BKMK_examples"></a>Exemplos
Para adicionar pacotes de driver a uma imagem de inicialização, digite um dos seguintes:
```
wdsutil /add-ImageDriverPackagemedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86 /Filtertype:DriverGroupName /Operator:Equal /Value:x86Bus /Filtertype:PackageProvider /Operator:Contains /Value:Provider1 /Filtertype:Packageversion /Operator:GreaterOrEqual /Value:6.1.0.0
```
```
wdsutil /verbose /add-ImageDriverPackagemedia: "WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```
```
wdsutil /verbose /add-ImageDriverPackagemedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Value:System /Value:DiskDrive /Value:HDC /Value:SCSIAdapter
```
#### <a name="additional-references"></a>Referências adicionais
[Chave de sintaxe de linha de comando](command-line-syntax-key.md)
[usando o comando add-ImageDriverPackage](using-the-add-imagedriverpackage-command.md)
[usando o subcomando add AllDriverPackages](using-the-add-alldriverpackages-subcommand.md)