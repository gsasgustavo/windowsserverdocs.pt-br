---
title: 'Notas de versão: problemas importantes no Windows Server, versão 1709'
description: Resume os problemas críticos que exigem solução alternativa para evitar falhas, congelamento, falha de instalação e perda de dados.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 04/23/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 4eebc498289a81c7f27fcf4b84d81ae13bc38e4f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861977"
---
# <a name="release-notes-important-issues-in-windows-server-version-1709"></a>Notas de versão: Problemas importantes no Windows Server, versão 1709

>Aplica-se a: Canal semestral do Windows Server

Essas notas de versão resumem os problemas mais importantes no sistema operacional do Windows Server&reg;, inclusive formas de evitar ou solucionar problemas, se forem conhecidos. Para saber mais sobre alterações planejadas, novos recursos e correções desta versão, confira [Novidades no Windows Server versão 1709](whats-new-in-windows-server-1709.md) e os comunicados das equipes de recursos específicos. Salvo indicação em contrário, cada problema reportado aplica-se a todas as edições e opções de instalação do Windows Server 2016.  

Este documento é atualizado continuamente. À medida que são descobertas questões críticas que exijam uma solução alternativa, elas são adicionadas, assim como novas soluções e correções assim que estiverem disponíveis.  
  
## <a name="storage-spaces-direct"></a>Espaços de Armazenamento Diretos
[comment]: # (ID: desconhecido; Emissor: stevenek; estado: aprovou)  
Os Espaços de Armazenamento Diretos não estão incluídos no Windows Server, versão 1709. Se você chamar *Enable-ClusterStorageSpacesDirect* ou o alias *Enable-ClusterS2D*, em um servidor executando o Windows Server, versão 1709, você receberá um erro com a mensagem "A operação solicitação não é suportada".

Também não há suporte para apresentar os servidores que executam o Windows Server, versão 1709, em uma implantação direta de Espaços de armazenamento diretos do Windows Server 2016.

O modelo de lançamento do Windows Server está oferecendo uma nova opção para se alinhar com versão semelhantes e manutenção de modelos de [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) e [Office 365 ProPlus](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US). As versões de Canal semestral oferecem novas funcionalidades para clientes que desejam mover em um ritmo rápido e terão novos lançamentos disponíveis duas vezes por ano, no primeiro e segundo semestres.

O canal de semestral do Windows Server se concentra em contêineres e inovação mais rápida se beneficiando de cenários de aplicativo, consulte esta [blog](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update) para obter informações adicionais. Clientes à procura de funções de infraestrutura, como espaços de armazenamento diretos, devem usar as versões de canal de manutenção em longo prazo, como o Windows Server 2016 (agora disponível) e [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (lançado posteriormente este ano). Estamos empenhados em criar a melhor plataforma para infraestrutura hiperconvergente, e continuaremos a desenvolver novos recursos e melhorar os existentes com base em seus comentários. 

Os Espaços de armazenamento diretos foram introduzidos no Windows Server 2016 e é a base para nossa plataforma com hiperconvergência. Estamos felizes pela adoção positiva da plataforma com hiperconvergência da Microsoft e estamos comprometidos com nossos clientes.

Estamos atentos aos seus comentários e estamos trabalhando para fornecer a [próximo conjunto de inovações](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/) para nossa plataforma hiperconvergente. Esses recursos estão disponíveis no [Windows Insiders](https://insider.windows.com/for-business/) compilações e podemos adoraria para você experimentá-los e compartilhe seus comentários. Para clientes que buscam uma solução com hiperconvergência validada, recomendamos o programa [definido pelo software do Windows Server](http://microsoft.com/wssd).