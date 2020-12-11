---
description: 'Saiba mais sobre: configurar o HGS para comunicações HTTPS'
title: Configurar o HGS para comunicações HTTPS
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: c28500d236625410961ef1ee3012001c1d277714
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049884"
---
# <a name="configure-hgs-for-https-communications"></a>Configurar o HGS para comunicações HTTPS

>Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016

Por padrão, quando você inicializar o servidor HGS, ele configurará os sites da Web do IIS para comunicações somente HTTP.
Todo material confidencial que está sendo transmitido para e do HGS é sempre criptografado usando a criptografia no nível da mensagem, no entanto, se você quiser um nível mais alto de segurança, também poderá habilitar o HTTPS Configurando o HGS com um certificado SSL.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)]

