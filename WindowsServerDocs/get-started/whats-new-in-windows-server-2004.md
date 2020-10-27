---
title: Novidades no Windows Server, versões 2004 e 20H2
description: Novos recursos do Windows Server, versões 2004 e 20H2.
ms.topic: article
author: Heidilohr
ms.author: helohr
ms.date: 05/27/2020
ms.localizationpriority: high
ms.openlocfilehash: f44dcc7a1c7fab2d99f0358794bd5b2aedb87b75
ms.sourcegitcommit: b82dfbfdc5df1327feb8be053a760739b01e3031
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92255863"
---
# <a name="whats-new-in-windows-server-version-2004-and-20h2"></a>Novidades no Windows Server, versão 2004 e 20H2

>Aplica-se a: Windows Server (Canal semestral)

Para saber mais sobre os recursos mais recentes do Windows, consulte [Novidades no Windows Server](whats-new-in-windows-server.md). Este tópico descreve alguns dos novos recursos do Windows Server, versões 2004 e 20H2.

O Windows Server, versão 20H2 é a próxima versão do Canal Semestral do Windows Server, versão 2004. Essa versão se concentra na confiabilidade, no desempenho e em outros aprimoramentos gerais, mas não tem novos recursos. Assim como ocorre com outras versões de Canal Semestral, o suporte para ela é de 18 meses a partir do lançamento. Para saber mais sobre as datas de suporte para as versões do Canal Semestral, confira as [informações de versão do Windows Server](windows-server-release-info.md).

## <a name="server-core-container-improvements"></a>Aprimoramentos no contêiner do Server Core

Reduzimos o tamanho total das imagens de contêiner do Server Core para melhorar o desempenho e as velocidades de download. Incluímos os seguintes aprimoramentos:

- A maioria das imagens NGEN foi removida da imagem de contêiner do Server Core para diminuir o tamanho dela.
- As imagens do runtime do .NET Framework criadas com base em imagens de contêiner do Server Core agora estão otimizadas para os aplicativos ASP.NET e para o desempenho de script do Windows PowerShell.
- A equipe do .NET também se certificou de que há apenas uma cópia de cada imagem NGEN, resultando em um tamanho menor de imagens do .NET Framework.

Para dar uma ideia melhor do tamanho desses contêineres, a tabela a seguir compara a versão atual do contêiner a partir da [atualização de segurança mensal de maio de 2020](https://support.microsoft.com/help/4561769/windows-server-containers-for-may-2020) (também conhecida como atualização "5B") com versões anteriores.

| Versão do contêiner | Tamanho do download | Tamanho em disco |
|---|---|---|
| Windows Server, versão 1903 | 2,311 GB | 5,1 GB |
| Windows Server, versão 1909 | 2,257 GB | 4,97 GB |
| Windows Server, versão 2004 | 1,830 GB | 3,98 GB |

Para obter mais informações sobre a atualização do Windows Server, versão 2004, confira [nossa postagem no blog](https://techcommunity.microsoft.com/t5/containers/windows-server-version-2004-now-available/ba-p/1419194). Para saber mais sobre as atualizações de contêiner do Windows em geral, confira [Atualizar contêineres do Windows Server](/virtualization/windowscontainers/deploy-containers/update-containers/).
