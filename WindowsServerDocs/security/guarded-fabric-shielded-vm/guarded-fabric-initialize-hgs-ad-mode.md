---
description: 'Saiba mais sobre: inicializar o HGS usando o atestado de administrador confiável'
title: Inicializar o HGS usando o atestado de administrador confiável
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 65ba0bd90d42ac038eeb8eb304def80ce7093ff1
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049754"
---
# <a name="initialize-hgs-using-admin-trusted-attestation"></a>Inicializar o HGS usando o atestado de administrador confiável

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

>[!IMPORTANT]
>O atestado confiável de administrador (modo de anúncio) é preterido a partir do Windows Server 2019. Para ambientes em que o atestado do TPM não é possível, configure o [atestado de chave do host](guarded-fabric-initialize-hgs-key-mode.md). O atestado de chave de host fornece garantia semelhante ao modo AD e é mais simples de configurar.


Essas etapas variam dependendo se você está inicializando o HGS em uma nova floresta ou em uma floresta de bastiões existente:

1. [Inicializar o cluster HGS em uma nova floresta (padrão)](guarded-fabric-initialize-hgs-ad-mode-default.md)

   -Ou-

   [Inicializar o cluster HGS em uma floresta de bastiões existente](guarded-fabric-initialize-hgs-ad-mode-bastion.md)

2. [Configurar o encaminhamento de DNS no domínio de malha](guarded-fabric-configuring-fabric-dns.md)

3. [Configurar o encaminhamento de DNS e uma relação de confiança unidirecional no domínio HGS](guarded-fabric-configure-dns-forwarding-and-trust.md)



