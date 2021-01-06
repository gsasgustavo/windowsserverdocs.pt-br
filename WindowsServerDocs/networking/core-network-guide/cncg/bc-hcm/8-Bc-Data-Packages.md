---
title: Criar pacotes de dados do servidor de conteúdo para conteúdo da Web e do arquivo (opcional)
description: Este guia fornece instruções sobre como implantar o BranchCache no modo de cache hospedado em computadores que executam o Windows Server 2016 e o Windows 10
manager: brianlic
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: e7b2ba5890eedb6da06977996a58cd67e529fd92
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947862"
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>Criar pacotes de dados do servidor de conteúdo para conteúdo da Web e do arquivo (opcional)

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Você pode usar este procedimento para fazer o hash de conteúdo em servidores Web e de arquivos e, em seguida, criar pacotes de dados para importar no servidor de cache hospedado.

Esse procedimento é opcional porque não é necessário prefazer hash e pré-carregar conteúdo em seus servidores de cache hospedados. Se você não pré-carregar o conteúdo, os dados são adicionados automaticamente ao cache hospedado, pois os clientes o baixam pela conexão WAN.

Este procedimento fornece instruções para o conteúdo de prehash em servidores de arquivos e servidores Web. Se você não tiver um desses tipos de servidores de conteúdo, não será necessário executar as instruções para esse tipo de servidor de conteúdo.

>[!IMPORTANT]
>Antes de executar esse procedimento, você deve instalar e configurar o BranchCache em seus servidores de conteúdo. Além disso, se você planeja alterar o segredo do servidor em um servidor de conteúdo, faça isso antes de fazer o hash de um \- conteúdo. a modificação do segredo do servidor invalida \- hashes gerados anteriormente.

Para executar esse procedimento, é necessário ser membro do grupo Administradores.

## <a name="to-create-content-server-data-packages"></a>Para criar pacotes de dados do servidor de conteúdo

1. Em cada servidor de conteúdo, localize as pastas e os arquivos que você deseja prehash e adicione a um pacote de dados. Identifique ou crie uma pasta na qual você deseja salvar o pacote de dados posteriormente neste procedimento.

2. No computador servidor, abra o Windows PowerShell com privilégios de administrador.

3. Execute um ou ambos os itens a seguir, dependendo dos tipos de servidores de conteúdo que você tem:

    > [!NOTE]
    > O valor do parâmetro – Path é a pasta na qual o conteúdo está localizado. Você deve substituir os valores de exemplo nos comandos abaixo por um local de pasta válido no servidor de conteúdo que contém os dados que você deseja prehash e adicionar a um pacote.

    - Se o conteúdo que você deseja prehash estiver em um servidor de arquivos, digite o comando a seguir e pressione ENTER.

        ```
        Publish-BCFileContent -Path D:\share -StageData
        ```

    -   Se o conteúdo que você deseja prehash estiver em um servidor Web, digite o comando a seguir e pressione ENTER.

        ```
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```

4. Crie o pacote de dados executando o comando a seguir em cada um dos seus servidores de conteúdo. Substitua o valor de exemplo \( D: \\ temp \) para o parâmetro – Destination pelo local que você identificou ou criou no início deste procedimento.

    ```
    Export-BCDataPackage –Destination D:\temp
    ```

5. No servidor de conteúdo, acesse o compartilhamento nos servidores de cache hospedados em que você deseja pré-carregar o conteúdo e copie os pacotes de dados para os compartilhamentos nos servidores de cache hospedados.

Para continuar com este guia, consulte [importar pacotes de dados no servidor de cache hospedado &#40;&#41;opcional ](9-Bc-Import-Data.md).

