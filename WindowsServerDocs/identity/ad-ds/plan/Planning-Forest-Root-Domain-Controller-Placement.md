---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: Planejando posicionamento do controlador de domínio raiz da floresta
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ab34eb19c880fbe22b9da74a6745d9277a564cb4
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93071058"
---
# <a name="planning-forest-root-domain-controller-placement"></a>Planejando posicionamento do controlador de domínio raiz da floresta

> Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Controladores de domínio raiz de floresta são necessários para criar caminhos de confiança para clientes que precisam acessar recursos em domínios diferentes do seu. Coloque os controladores de domínio raiz da floresta em locais de Hub e em locais que hospedam datacenters. Se os usuários em um determinado local precisarem acessar recursos de outros domínios no mesmo local e a disponibilidade de rede entre o datacenter e o local do usuário não for confiável, você poderá adicionar um controlador de domínio raiz da floresta no local ou criar uma relação de confiança de atalho entre os dois domínios. É mais econômico criar uma relação de confiança de atalho entre os domínios, a menos que você tenha outros motivos para posicionar um controlador de domínio raiz de floresta nesse local.

As relações de confiança de atalho ajudam a otimizar as solicitações de autenticação feitas de usuários localizados em qualquer domínio. Para obter mais informações sobre as relações de confiança de atalho entre domínios, consulte o artigo [noções básicas sobre quando criar uma relação de confiança de atalho](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc754538(v=ws.11)).

Para uma planilha para ajudá-lo a documentar o posicionamento do controlador de domínio raiz da floresta, consulte [ajudas de trabalho para o Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), baixar Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip e abrir "posicionamento do controlador de domínio" (DSSTOPO_4.doc).

Você precisará consultar essas informações ao criar o domínio raiz da floresta. Para obter mais informações sobre como implantar o domínio raiz da floresta, consulte [implantando um domínio raiz da floresta do Windows Server 2008](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10)).
