---
title: Importar pacotes de dados no servidor de cache hospedado (opcional)
description: Este guia fornece instruções sobre como implantar o BranchCache no modo de cache hospedado em computadores que executam o Windows Server 2016 e o Windows 10
manager: brianlic
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 8812c3008c2563fb8b436740d9fc0116c87c0154
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950212"
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>Importar pacotes de dados no servidor de cache hospedado \( opcional\)

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Você pode usar este procedimento para importar pacotes de dados e pré-carregar conteúdo em seus servidores de cache hospedados.

Esse procedimento é opcional porque não é necessário prefazer hash e pré-carregar conteúdo em seus servidores de cache hospedados.

Se você não carregar o \- conteúdo previamente, os dados serão adicionados ao cache hospedado automaticamente, pois os clientes o baixarão pela conexão WAN.

Você deve ser membro do grupo Administradores para executar esse procedimento.

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>Para importar pacotes de dados no servidor de cache hospedado

1. No computador servidor, abra o Windows PowerShell com privilégios de administrador.

2. Digite o comando a seguir, substituindo o valor do parâmetro – Path pelo local da pasta em que você armazenou seus pacotes de dados e, em seguida, pressione ENTER.

    ```
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```

3. Se você tiver mais de um servidor de cache hospedado no qual deseja pré-carregar o conteúdo, execute este procedimento em cada servidor de cache hospedado.

Para continuar com este guia, consulte [Configurar descoberta automática de cache hospedado pelo cliente por ponto de conexão de serviço](10-Bc-Client-By-Scp.md).
