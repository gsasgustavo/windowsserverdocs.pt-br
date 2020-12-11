---
description: 'Saiba mais sobre: Implantando proxies herdados do servidor de Federação AD FS'
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: Implantando proxies de servidor de Federação no AD FS
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 7798867f8445ee99835e883ccab771fa346b2673
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044124"
---
# <a name="deploying-legacy-ad-fs-federation-server-proxies"></a>Implantando proxies de servidor de Federação AD FS herdados

Para implantar proxies de servidor de Federação no Serviços de Federação do Active Directory (AD FS) \( AD FS \) , conclua cada uma das tarefas na [lista de verificação: Configurando um proxy de servidor de Federação](Checklist--Setting-Up-a-Federation-Server-Proxy.md).

> [!NOTE]
> Ao usar essa lista de verificação, recomendamos que você leia primeiro as referências às diretrizes de planejamento de proxy do servidor de Federação no [Guia de design de AD FS no Windows server 2012](../design/ad-fs-design-guide-in-windows-server-2012.md) antes de iniciar os procedimentos para configurar os servidores. Seguir a lista de verificação fornece uma compreensão melhor do processo de design e implantação para proxies de servidor de Federação.

## <a name="about-federation-server-proxies"></a>Sobre proxies de servidor de Federação
Os proxies do servidor de Federação são computadores que executam o Windows Server &reg; 2012 e AD FS software que foram configurados manualmente para atuar na função de proxy. Você pode usar proxies de servidor de federação em sua organização para fornecer serviços intermediários entre um cliente de Internet e um servidor de federação por trás de um firewall em sua rede corporativa.

> [!NOTE]
> Embora o servidor de Federação e as funções de proxy do servidor de Federação não possam ser instalados no mesmo computador, um servidor de Federação pode executar funções de proxy do servidor de Federação. Para obter mais informações, consulte [When to Create a Federation Server](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807101(v=ws.11)).

O ato de instalar o software AD FS em um computador com Windows Server &reg; 2012 e configurá-lo para servir na função de proxy torna esse computador um proxy de servidor de Federação.

