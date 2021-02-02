---
title: Noções básicas sobre extensões do Windows Admin Center
description: Noções básicas sobre as extensões do SDK do Windows Admin Center (Project Honolulu)
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 578376a10b83466382bf9e02f91ff94656bd6c88
ms.sourcegitcommit: 84b97d34d606b6bf4b6ec8760a93107f1b311428
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99245473"
---
# <a name="understanding-windows-admin-center-extensions"></a>Noções básicas sobre extensões do Windows Admin Center

>Aplica-se a: Windows Admin Center, Versão prévia do Windows Admin Center

Caso você ainda não esteja familiarizado com o funcionamento do centro de administração do Windows, vamos começar com a arquitetura de alto nível. O Windows Admin Center é composto por dois componentes principais:

- Um **serviço Web** leve que serve de páginas da Web da interface do usuário do Windows Admin Center às solicitações de navegador.
- **Componente de gateway** que escuta solicitações da API REST das páginas da Web e retransmite chamadas WMI ou scripts do PowerShell para ser executado em um servidor de destino ou cluster.

![Um diagrama de uma arquitetura do centro de administração do Windows.](../media/understand-extensions/wac-architecture-500px.png)

As páginas da web de IU de Windows Admin Center atendido pelo serviço web tem dois componentes principais de interface do usuário de uma perspectiva de extensibilidade, soluções e ferramentas, que são implementadas como extensões, e, em um terceiro tipo de extensão chamado plug-ins do gateway.

## <a name="solution-extensions"></a>Extensões de solução

Na tela inicial do Windows Admin Center, por padrão, você pode adicionar conexões que são de um dos quatro tipos: Windows Server, conexões de computador Windows, conexões de cluster de failover e conexões de cluster de hiperconvergência. Depois que uma conexão é adicionada, o nome da conexão e tipo serão exibidas na tela inicial. Clicar no nome da conexão resulta na tentativa de conexão ao servidor de destino ou cluster e depois no carregamento da interface do usuário da conexão.

![Captura de tela do recurso Adicionar conexões do centro de administração do Windows.](../media/understand-extensions/solutions-ui.png)

Cada um desses tipos de conexão mapeia para uma solução e soluções são definidas por meio de um tipo de extensão chamado extensões de "solução". Soluções geralmente definem um tipo exclusivo do objeto que você deseja gerenciar por meio do Windows Admin Center, como servidores, PCs ou clusters de failover. Você também pode definir uma nova solução para conectar e gerenciar outros dispositivos, como comutadores de rede e servidores Linux ou mesmo serviços como Serviços de Área de Trabalho Remota.

## <a name="tool-extensions"></a>Extensões de ferramenta

Quando você clicar em uma conexão na tela inicial do Windows Admin Center e conectar, a extensão de solução para o tipo de conexão selecionados será carregada e, em seguida, serão apresentados com a solução de interface do usuário, incluindo uma lista de ferramentas no painel de navegação à esquerda. Quando você clica em uma ferramenta, a ferramenta de interface do usuário é carregada e exibida no painel direito.

![Arquitetura de IU de Windows Admin Center](../media/understand-extensions/ui-architecture.png)

Cada uma dessas ferramentas são definidas por meio de um segundo tipo de extensão chamada de extensões "ferramentas". Quando uma ferramenta é carregada, ela pode executar chamadas WMI ou scripts do PowerShell em um servidor de destino ou cluster e exibir informações na interface do usuário ou executar comandos com base na entrada do usuário. Uma extensão de ferramenta define quais soluções que devem ser exibidas, resultando em um conjunto diferente de ferramentas para cada solução. Se estiver criando uma nova extensão de solução, você precisará gravar uma ou mais extensões de ferramenta que fornecem funcionalidade para a solução.

![Lista de ferramentas para cada solução](../media/understand-extensions/tools-for-solutions.png)

## <a name="gateway-plugins"></a>Plug-ins do gateway

O serviço de gateway expõe APIs REST para a interface do usuário chamar e retransmite comandos e scripts a ser executado no destino. O serviço de gateway pode ser estendido pelo gateway plug-ins que oferecem suporte aos protocolos diferentes. O Windows Admin Center vem com dois gateway plug-ins, um para a execução de scripts do PowerShell e outro para os comandos WMI. Se você precisar se comunicar com o destino por meio de um protocolo diferente do PowerShell ou WMI, como REST, você pode construir um plug-in do gateway para isso.

## <a name="next-steps"></a>Próximas etapas

Dependendo de quais recursos você deseja compilar no Windows Admin Center, a [criação de uma extensão de ferramenta](develop-tool.md) para um servidor existente ou a solução de cluster pode ser suficiente e é a primeira etapa mais fácil para a criação de extensões. No entanto, se o recurso está disponível para gerenciar um dispositivo, serviço ou algo completamente novo, em vez de um servidor ou cluster, você deve considerar [a criação de uma extensão de solução](develop-solution.md) com uma ou mais ferramentas. E, por fim, se você precisar se comunicar com o destino por meio de um protocolo diferente do WMI ou do PowerShell, você precisará [criar um plug-in de gateway](develop-gateway-plugin.md). [Continue lendo](developing-extensions.md) para saber como configurar seu ambiente de desenvolvimento e começar a gravar sua extensão primeiro.
