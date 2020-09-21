---
title: 'Notas sobre a versão: problemas importantes no Windows Server, versão 1709'
description: Resume os problemas críticos que exigem solução alternativa para evitar falhas, congelamento, falha de instalação e perda de dados.
ms.date: 04/23/2018
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: f707dbbe22624489f9c5939987ea9831cc467214
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766699"
---
# <a name="release-notes-important-issues-in-windows-server-version-1709"></a>Notas sobre a versão: Problemas importantes no Windows Server, versão 1709

>Aplica-se a: Windows Server Canal Semestral

Essas notas sobre a versão resumem os problemas mais importantes no sistema operacional do Windows Server&reg;, inclusive formas de evitar ou solucionar problemas, se forem conhecidos. Para saber mais sobre alterações planejadas, novos recursos e correções desta versão, confira [Novidades no Windows Server versão 1709](whats-new-in-windows-server-1709.md) e os comunicados das equipes de recursos específicos. Salvo indicação em contrário, cada problema reportado aplica-se a todas as edições e opções de instalação do Windows Server 2016.

Este documento é atualizado continuamente. À medida que são descobertas questões críticas que exijam uma solução alternativa, elas são adicionadas, assim como novas soluções e correções assim que estiverem disponíveis.

## <a name="storage-spaces-direct"></a>Espaços de Armazenamento Direct
[comment]: # (ID: desconhecido; remetente: stevenek; estado: aprovado)
Os Espaços de Armazenamento Diretos não estão incluídos no Windows Server, versão 1709. Se você chamar *Enable-ClusterStorageSpacesDirect* ou o alias *Enable-ClusterS2D* em um servidor que executa o Windows Server, versão 1709, você receberá um erro com a mensagem Não há suporte para a operação solicitada.

Também não há suporte para apresentar os servidores que executam o Windows Server, versão 1709, em uma implantação de Espaços de Armazenamento Diretos do Windows Server 2016.

O modelo de lançamento do Windows Server está oferecendo uma nova opção para se alinhar com modelos de versão e de manutenção semelhantes do [Windows 10](/windows/deployment/update/waas-overview) e de [Aplicativos do Microsoft 365](/DeployOffice/overview-update-channels). As versões de Canal Semestral oferecem novas funcionalidades para clientes que desejam mover em um ritmo rápido e terão novos lançamentos disponíveis duas vezes por ano, no primeiro e segundo semestres.

O Canal Semestral do Windows Server se concentra em contêineres e cenários de aplicativo, beneficiando-se da inovação mais rápida. Confira este [blog](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update) para obter informações adicionais. Clientes em busca de funções de infraestrutura, como Espaços de Armazenamento Diretos, devem usar as versões de Canal de Manutenção em Longo Prazo, como o Windows Server 2016 (agora disponível) e o [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (a ser lançado posteriormente neste ano). Estamos empenhados em criar a melhor plataforma para infraestrutura hiperconvergente e continuaremos a desenvolver novos recursos e melhorar os existentes com base em seus comentários.

Os Espaços de Armazenamento Diretos foram introduzidos no Windows Server 2016 e são a base para nossa plataforma com hiperconvergência. Estamos felizes pela adoção positiva da plataforma com hiperconvergência da Microsoft e estamos comprometidos com nossos clientes.

Escutamos os seus comentários e estamos trabalhando para fornecer o [próximo conjunto de inovações](https://cloudblogs.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/) para nossa plataforma com hiperconvergência. Esses recursos estão disponíveis atualmente nos builds para [Participantes do Programa Windows Insider](https://insider.windows.com/for-business/) e gostaríamos muito que você experimente-os e compartilhe comentários. Para clientes que buscam uma solução com hiperconvergência validada, recomendamos o programa [definido pelo software do Windows Server](https://microsoft.com/wssd).