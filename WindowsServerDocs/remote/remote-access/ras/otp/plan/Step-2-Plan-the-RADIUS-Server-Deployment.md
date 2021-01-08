---
title: Etapa 2 planejar a implantação do servidor RADIUS
description: Saiba como planejar o servidor de autenticação de senha de uso único (OTP).
manager: brianlic
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 5658c4c3a323bf9e0df5af8cf57dad85d98fe8dd
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040156"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>Etapa 2 planejar a implantação do servidor RADIUS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Depois de implantar um único servidor de acesso remoto, planeje o servidor de autenticação OTP (senha de uso único).

|Tarefa|Descrição|
|----|--------|
|2,1 planejar o servidor RADIUS|Para o servidor de autenticação OTP, o acesso remoto no Windows Server 2016 e no Windows Server 2012 dá suporte a qualquer servidor de OTP habilitado para RADIUS que dá suporte ao protocolo PAP.|

## <a name="21-plan-the-radius-server"></a><a name="BKMK_1.1"></a>2,1 planejar o servidor RADIUS
Observe o seguinte ao planejar um servidor RADIUS para autenticação OTP:

-   Para a maioria dos tipos de implantações de OTP, você deve configurar o servidor de acesso remoto como um agente RADIUS. Para obter mais informações, consulte a documentação do fornecedor de OTP.

-   Para todas as implantações de OTP, você deve sincronizar seus Active Directory usuários com o servidor RADIUS.

-   O servidor RADIUS não precisa ser um membro do domínio.

-   Ao implantar o servidor RADIUS, você configura um segredo compartilhado e o número da porta para o tráfego RADIUS. Anote esses detalhes; Eles são necessários quando você configura o servidor de acesso remoto.

Você pode exibir um exemplo de guia de laboratório de teste que configura a autenticação de OTP com um servidor RSA SecurID no [Guia de laboratório de teste: demonstre o DirectAccess com autenticação OTP e RSA SecurID](../../../directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid.md).



