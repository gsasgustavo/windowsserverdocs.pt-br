---
title: Mover e redimensionar o cache hospedado (opcional)
description: Este guia fornece instruções sobre como implantar o BranchCache no modo de cache hospedado em computadores que executam o Windows Server 2016 e o Windows 10
manager: brianlic
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 276ab47bc6f4f906aaeafc7779c4e2afdb80b260
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947882"
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>Mover e redimensionar o cache hospedado \( opcional\)

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Você pode usar este procedimento para mover o cache hospedado para a unidade e a pasta que preferir, e para especificar a quantidade de espaço em disco que o servidor de cache hospedado pode usar para o cache hospedado.

Esse procedimento é opcional. Se o local do cache padrão \( % windir% \\ UserProfiles \\ NetworkService \\ AppData \\ local \\ PeerDistPub \) e Size – que é 5% do espaço total no disco rígido – são apropriados para sua implantação, você não precisa alterá-los.

Você deve ser membro do grupo Administradores para executar esse procedimento.

### <a name="to-move-and-resize-the-hosted-cache"></a>Para mover e redimensionar o cache hospedado

1. Abra o Windows PowerShell com privilégios de administrador.

2. Digite o seguinte comando para mover o cache hospedado para outro local no computador local e pressione ENTER.

    > [!IMPORTANT]
    > Antes de executar o comando a seguir, substitua os valores de parâmetro, como – Path e – MoveTo, por valores que são apropriados para sua implantação.

    ```
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ```

3.  Digite o seguinte comando para redimensionar o cache hospedado – especificamente, o DataCache \- no computador local. Pressione ENTER.

    > [!IMPORTANT]
    > Antes de executar o comando a seguir, substitua os valores de parâmetro, como \- percentual, por valores que são apropriados para sua implantação.

    ```
    Set-BCCache -Percentage 20
    ```

4.  Para verificar a configuração do servidor de cache hospedado, digite o comando a seguir e pressione ENTER.

    ```
    Get-BCStatus
    ```

    Os resultados do status de exibição do comando para todos os aspectos da instalação do BranchCache. A seguir estão algumas das configurações do BranchCache e o valor correto para cada item:

    -   DataCache | CacheFileDirectoryPath: exibe o local do disco rígido que corresponde ao valor fornecido com o parâmetro – MoveTo do comando SetBCCache. Por exemplo, se você forneceu o valor D: \\ DataCache, esse valor será exibido na saída do comando.

    -   DataCache | MaxCacheSizeAsPercentageOfDiskVolume: exibe o número que corresponde ao valor fornecido com o parâmetro – Percentage do comando SetBCCache. Por exemplo, se você forneceu o valor 20, esse valor é exibido na saída do comando.

Para continuar com este guia, consulte [prehash e pré-carregar conteúdo no servidor de cache hospedado &#40;&#41;opcional ](7-Bc-Prehash-Preload.md).