---
title: Planejar uma implantação multissite
description: Saiba mais sobre as etapas de planejamento necessárias para implantar o acesso remoto do Windows Server 2016 ou do Windows Server 2012 em uma configuração multissite.
manager: brianlic
ms.topic: article
ms.assetid: 8387eabe-7363-4367-b5b1-03c67baa2933
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: a4a56e430b1b40627aaf0e387c8df8ec122b94fb
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97941632"
---
# <a name="plan-a-multisite-deployment"></a>Planejar uma implantação multissite

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

 O Windows Server 2016, Windows Server 2012 combina DirectAccess e roteamento e VPN RRAS (serviço de acesso remoto) em uma única função de acesso remoto. Esta visão geral fornece uma introdução às etapas de planejamento necessárias para implantar o acesso remoto do Windows Server 2016 ou do Windows Server 2012 em uma configuração multissite.

1.  [Implante um único servidor DirectAccess com configurações avançadas](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831436(v=ws.11)). Esta etapa inclui o planejamento da infraestrutura necessária para implantar um único servidor. Ele inclui o planejamento de configurações de rede e servidor, requisitos de certificado, configurações de DNS, implantação de servidor de local de rede, servidores de gerenciamento do DirectAccess, configurações de Active Directory e objetos de Política de Grupo (GPOs).

2.  [Etapa 2 planejar a infraestrutura multissite](Step-2-Plan-the-Multisite-Infrastructure.md). Esta etapa inclui o planejamento de Active Directory e GPO e a configuração de DNS.

3.  [Etapa 3 planejar a implantação multissite](Step-3-Plan-the-Multisite-Deployment.md). Esta etapa inclui o planejamento de configurações de certificado, configuração de servidor de local de rede, configurações de ponto de entrada de cliente, configurações de prefixo IPv6 e, opcionalmente, configurações de balanceamento de carga global.

> [!NOTE]
> Registre suas decisões de planejamento para a implantação avançada de acesso remoto. Esse registro pode ser usado como um auxílio de trabalho para todos os envolvidos na conclusão das etapas de implantação.

Depois de concluir essas etapas de planejamento, consulte [Configurando uma implantação multissite](../configure/Configure-a-Multisite-Deployment.md).

