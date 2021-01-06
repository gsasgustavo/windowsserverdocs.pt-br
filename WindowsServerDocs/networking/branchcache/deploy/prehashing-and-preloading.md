---
title: Realizar o hash prévio e o pré-carregamento de conteúdo em servidores de cache hospedado (opcionais)
description: Saiba como forçar a criação de informações de conteúdo – também chamadas de hashes-em servidores Web e de arquivos habilitados para BranchCache.
manager: brianlic
ms.topic: how-to
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: d903338f58cd7a01967902243f79f4eb28e58882
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97942502"
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>Realizar o hash prévio e o pré-carregamento de conteúdo em servidores de cache hospedado (opcionais)

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para forçar a criação de informações de conteúdo – também chamadas de hashes-em servidores Web e de arquivos habilitados para BranchCache. Você também pode reunir os dados em arquivos e servidores Web em pacotes que podem ser transferidos para servidores de cache hospedados remotos.  Isso fornece a capacidade de pré-carregar conteúdo em servidores de cache hospedados remotos para que os dados estejam disponíveis para o primeiro acesso para cliente.

Você deve ser membro de **Administradores** ou equivalente para executar este procedimento.

### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>Para colocar o conteúdo de pré-hash e pré-carregar o conteúdo em servidores de cache hospedados

1.  Faça logon no arquivo ou servidor Web que contém os dados que você deseja pré-carregar e identifique as pastas e os arquivos que você deseja carregar em um ou mais servidores de cache hospedados remotamente.

2.  Execute o Windows PowerShell como administrador. Para cada pasta e arquivo, execute o `Publish-BCFileContent` comando ou o `Publish-BCWebContent` comando, dependendo do tipo de servidor de conteúdo, para disparar a geração de hash e para adicionar dados a um pacote de dados.

3.  Depois que todos os dados tiverem sido adicionados ao pacote de dados, exporte-os usando o `Export-BCCachePackage` comando para produzir um arquivo de pacote de dados.

4.  Mova o arquivo de pacote de dados para os servidores de cache hospedado remoto usando sua opção de tecnologia de transferência de arquivo.  FTP, SMB, HTTP, DVD e discos rígidos portáteis são Transportações viáveis.

5.  Importe o arquivo de pacote de dados nos servidores de cache hospedados remotos usando o `Import-BCCachePackage` comando.


