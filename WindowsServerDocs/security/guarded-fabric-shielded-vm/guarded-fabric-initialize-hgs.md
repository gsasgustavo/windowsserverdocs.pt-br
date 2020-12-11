---
description: 'Saiba mais sobre: inicializar o serviço guardião de host (HGS)'
title: Inicializar HGS
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: f2dc8999a851aa3830a0ffb8e17c3eb9909fe2d1
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97047254"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>Inicializar o serviço guardião de host (HGS)

>Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016

Ao inicializar o HGS, você especifica o modo que o HGS usará para medir a integridade dos hosts protegidos. Há duas opções mutuamente exclusivas. Para obter informações básicas sobre qual modo escolher, consulte [malha protegida e guia de planejamento de VM blindada para hosters](guarded-fabric-planning-for-hosters.md).

Os tópicos a seguir abrangem as etapas de implantação para cada modo:

- [TPM-atestado confiável (modo TPM)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [Atestado de chave de host (modo de chave)](guarded-fabric-initialize-hgs-key-mode.md)
- [Administrador-atestado confiável (modo de AD)](guarded-fabric-initialize-hgs-ad-mode.md)

Você deve executar essas etapas em um servidor físico.
