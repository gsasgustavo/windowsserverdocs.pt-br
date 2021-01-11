---
title: Alterações no Nano Server no Canal Semestral do Windows Server
description: No novo modelo de manutenção do Windows Server, o Nano Server é um contêiner apenas do sistema operacional, com algumas alterações de recurso.
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 05/21/2019
ms.topic: how-to
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: f8495867c63482e14add82f72959d8a73b5ec1a6
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946752"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Alterações no Nano Server no Canal Semestral do Windows Server

>Aplica-se a: Windows Server, Canal Semestral

Se você já estiver executando o Nano Server, o modelo de serviços do [Canal Semestral do Windows Server](../get-started-19/servicing-channels-19.md) será familiar, pois foi atendido anteriormente pelo modelo de CBB (Branch Atual para Negócios). O Canal Semestral do Windows Server é apenas um novo nome para o mesmo modelo. Nesse modelo, espera-se versões de atualização de recurso do Nano Server de duas a três vezes por ano.

No entanto, começando com o Windows Server versão 1803, o Nano Server está disponível somente como uma **imagem de sistema operacional base do contêiner**. Você precisa executá-lo como um contêiner em um host de contêiner, tal como uma instalação Server Core do Windows Server. A execução de um contêiner com base no Nano Server nesta versão difere de versões anteriores das seguintes maneiras:

- O Nano Server foi otimizado para aplicativos .NET Core.
- O Nano Server é ainda menor que a versão do Windows Server 2016.
- O PowerShell Core, o .NET Core e o WMI não estão mais incluídos por padrão, mas você pode incluir pacotes de contêiner do [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) e [.NET Core](https://hub.docker.com/r/microsoft/dotnet/) ao criar seu contêiner.
- Não há mais uma pilha de atendimento incluída no Nano Server. A Microsoft publica um contêiner Nano atualizado no Docker Hub que você reimplanta.
- Você soluciona os problemas do novo Contêiner Nano usando o Docker.
- Agora você pode executar contêineres Nano no IoT Core.

## <a name="related-topics"></a>Tópicos relacionados

- [Documentação de contêineres do Windows](/virtualization/windowscontainers/)
- [Visão geral do Canal Semestral do Windows Server](../get-started-19/servicing-channels-19.md)