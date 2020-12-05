---
title: WDSUTIL Get-AllDriverPackages
description: Artigo de referência do comando WDSUTIL Get-AllDriverPackages, que exibe informações sobre todos os pacotes de driver em um servidor que correspondem aos critérios de pesquisa especificados.
ms.topic: reference
ms.assetid: 9eb8fcb7-ef46-4c8d-9623-8969a3c8b8a4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dd144d9abc2776f7e56913efd40775c1eef4d3ac
ms.sourcegitcommit: 28b5ab74cb0b40539ccc1a83998d6391e87fe51f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96614918"
---
# <a name="wdsutil-get-alldriverpackages"></a>WDSUTIL Get-AllDriverPackages

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exibe informações sobre todos os pacotes de driver em um servidor que correspondem aos critérios de pesquisa especificados.

## <a name="syntax"></a>Sintaxe

```
wdsutil /get-alldriverpackages [/server:<servername>] [/show:{drivers | files | all}] [/filtertype:<filtertype> /operator:{equal | notequal | greaterorequal | lessorequal | contains} /value:<value> [/value:<value> ...]]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| `[/server:<servername>] `| O nome do servidor. Pode ser o nome NetBIOS ou o FQDN. Se um nome de servidor não for especificado, o servidor local será usado. |
| `[/show:{drivers | files | all}]` | Indica as informações do pacote a serem exibidas. Se **/show** não for especificado, o padrão será retornar apenas os metadados do pacote de driver. **Drivers** exibe a lista de drivers no pacote, os **arquivos** exibem a lista de arquivos no pacote e **todos** exibem drivers e arquivos. |
| `/filtertype:<filtertype>` | Especifica o atributo do pacote de driver a ser pesquisado. Você pode especificar vários atributos em um único comando. Você também deve especificar **/Operator** e **/Value** com essa opção.<p>O `<filtertype>` pode ser um dos seguintes:<ul><li>PackageId</li><li>PackageName</li><li>PackageEnabled</li><li>Packagedateadded</li><li>PackageInfFilename</li><li>PackageClass</li><li>PackageProvider</li><li>PackageArchitecture</li><li>PackageLocale</li><li>PackageSigned</li><li>PackagedatePublished</li><li>Packageversion</li><li>Driverdescription</li><li>DriverManufacturer</li><li>DriverHardwareId</li><li>DrivercompatibleId</li><li>DriverGroupId</li><li>DriverGroupName</li></ul> |
| `/operator:{equal | notequal | greaterorequal | lessorequal | contains}` | Especifica a relação entre o atributo e os valores. Você pode especificar **Contains** somente com atributos de cadeia de caracteres. Você pode especificar **greaterorequal** e **lessorequal** somente com atributos de data e versão. |
| `/value:<value>` | Especifica o valor a ser pesquisado para o especificado `<attribute>` . Você pode especificar vários valores para um único **/FilterType**. A lista abaixo descreve os atributos que você pode especificar para cada filtro. Para obter mais informações sobre esses atributos, consulte [atributos de driver e pacote](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759262(v=ws.11)). Os atributos podem incluir:<ul><li>**PackageId.** Especifica um GUID válido. Por exemplo: {4D36E972-E325-11CE-BFC1-08002BE10318}.</li><li>**PackageName.** Especifica qualquer valor de cadeia de caracteres.</li><li>**PackageEnabled.** Especifica *Sim* ou *não*.</li><li>**Packagedateadded.** Especifica a data no seguinte formato: AAAA/MM/DD</li><li>**PackageInfFilename.** Especifica qualquer valor de cadeia de caracteres.</li><li>**PackageClass.** Especifica um nome de classe ou GUID de classe válido. Por exemplo: *DiskDrive*, *net* ou *{4D36E972-E325-11CE-BFC1-08002BE10318}*.</li><li>**PackageProvider.** Especifica qualquer valor de cadeia de caracteres.</li><li>**PackageArchitecture.** Especifica *x86*, *x64* ou *IA64*.</li><li>**PackagLocale.** Especifica um identificador de idioma válido. Por exemplo: *en-US* ou *es-es*.</li><li>**PackageSigned.** Especifica **Sim** ou **não**.</li><li>**PackagedatePublished.** Especifica a data no seguinte formato: AAAA/MM/DD.</li><li>**Packageversion.** Especifica a versão no seguinte formato: a.b.x.y. Por exemplo: 6.1.0.0.</li><li>**Driverdescription.** Especifica qualquer valor de cadeia de caracteres.</li><li>**DriverManufacturer.** Especifica qualquer valor de cadeia de caracteres.</li><li>**DriverHardwareId.** Especifica qualquer valor de cadeia de caracteres.</li><li>**DrivercompatibleId.** Especifica qualquer valor de cadeia de caracteres.</li><li>**DriverExcludeId.** Especifica qualquer valor de cadeia de caracteres.</li><li>**DriverGroupId.** Especifica um GUID válido. Por exemplo: {4D36E972-E325-11CE-BFC1-08002BE10318}.</li><li>**DriverGroupName.** Especifica qualquer valor de cadeia de caracteres.</li></ul> |

## <a name="examples"></a>Exemplos

Para exibir informações, digite:

```
wdsutil /get-alldriverpackages /server:MyWdsServer /show:all /filtertype:drivergroupname /operator:contains /value:printer /filtertype:packagearchitecture /operator:equal /value:x64 /value:x86
```

```
wdsutil /get-alldriverpackages /show:drivers /filtertype:packagedateadded /operator:greaterorequal /value:2008/01/01
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando WDSUTIL Get-DriverPackage](wdsutil-get-driverpackage.md)

- [comando WDSUTIL Get-driverpackagefile](wdsutil-get-driverpackagefile.md)
