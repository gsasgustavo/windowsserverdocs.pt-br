---
title: Planejar acesso remoto com autenticação OTP
description: Este tópico faz parte do guia implantar o acesso remoto com autenticação OTP no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: e4b171c628259abe59a6954ef9936b025f10c28e
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950272"
---
# <a name="plan-remote-access-with-otp-authentication"></a>Planejar acesso remoto com autenticação OTP

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

 O Windows Server 2016 e o Windows Server 2012 combinam o DirectAccess e o serviço de roteamento e acesso remoto (RRAS) para uma única função de acesso remoto. Esta visão geral fornece uma introdução às etapas de configuração necessárias para implantar uma única implantação de multissite de acesso remoto do Windows Server 2016 ou Windows Server 2012.


-  Etapa 1: [implantar um único servidor DirectAccess com configurações avançadas](../../../directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings.md). Esta etapa inclui o planejamento da infraestrutura necessária para implantar um único servidor. Ele inclui o planejamento de configurações de rede e servidor, requisitos de certificado, configurações de DNS, implantação de servidor de local de rede, servidores de gerenciamento do DirectAccess, configurações de Active Directory e objetos de Política de Grupo (GPOs).

-   [Etapa 2: planejar a implantação do servidor RADIUS](Step-2-Plan-the-RADIUS-Server-Deployment.md)

-   [Etapa 3: planejar a implantação de certificado de OTP](Step-3-Plan-OTP-Certificate-Deployment.md)

-   [Etapa 4: planejar a OTP no servidor de acesso remoto](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)

Depois de concluir essas etapas de planejamento, consulte [Configurar o acesso remoto com autenticação OTP](../configure/configure-ra-with-otp-authentication.md). Para obter informações sobre como configurar uma implantação multissite como uma prova de conceito em um ambiente de laboratório, consulte [Guia de laboratório de teste: demonstre o DirectAccess com autenticação de OTP e RSA SecurID](../../../directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid.md).

