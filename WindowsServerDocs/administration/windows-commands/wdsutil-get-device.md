---
title: WDSUTIL Get – Device
description: Artigo de referência para o WDSUTIL Get-Device, que recupera as informações dos serviços de implantação do Windows sobre um computador pré-configurado (ou seja, um computador físico que foi embutido em uma conta de computador nos serviços de domínio Active Directory.
ms.topic: reference
ms.assetid: 1da79286-7e1d-45f2-aea2-d446e16a6911
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 875ab5053ebbb1708f7b51896c9d82b9eba8f725
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91729652"
---
# <a name="wdsutil-get-device"></a>WDSUTIL Get – Device

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Recupera as informações dos serviços de implantação do Windows sobre um computador pré-configurado (ou seja, um computador físico que foi embutido em uma conta de computador nos serviços de domínio Active Directory.

## <a name="syntax"></a>Sintaxe
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
### <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
|Vice<Device name>|Especifica o nome do computador (SAMAccountName).|
|Sessão<MAC or UUID>|Especifica o endereço MAC ou o UUID (GUID) do computador, conforme mostrado nos exemplos a seguir. Observe que um GUID válido deve estar em um dos dois formatos de cadeia de caracteres binária ou de GUID<p>-   **Cadeia de caracteres binária**:/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6<br />-   **Endereço MAC**: 00B056882FDC (sem traços) ou 00-B0-56-88-2F-DC (com traços)<br />-   **Cadeia de caracteres GUID**:/ID: E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6|
|[/Domain: <Domain> ]|Especifica o domínio a ser procurado para o computador pré-configurado. O valor padrão para esse parâmetro é o domínio local.|
|[/Forest: {Sim &#124; não}]|Especifica se os serviços de implantação do Windows devem Pesquisar toda a floresta ou o domínio local. O valor padrão é **não**, o que significa que somente o domínio local será pesquisado.|
## <a name="examples"></a>Exemplos
Para obter informações usando o nome do computador, digite:
```
wdsutil /Get-Device /Device:computer1
```
Para obter informações usando o endereço MAC, digite:
```
wdsutil /verbose /Get-Device /ID:00-B0-56-88-2F-DC /Domain:MyDomain
```
Para obter informações usando a cadeia de caracteres GUID, digite:
```
wdsutil /verbose /Get-Device /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6 /forest:Yes
```
## <a name="additional-references"></a>Referências adicionais
- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
- [WDSUTIL Set-comando de dispositivo](wdsutil-set-device.md)
- [comando de adição de dispositivo WDSUTIL](wdsutil-add-device.md)
- [comando WDSUTIL Get-meus dispositivos](wdsutil-get-alldevices.md)
