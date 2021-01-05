---
title: Solucionar problemas do firewall no Windows Server Essentials
description: Saiba como usar o assistente para reparar acesso em qualquer local se você tiver problemas com o acesso remoto.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 51d94b67-8b9b-4159-80dd-f652d73a43cb
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 3cf84844a0bbca8128df1429c843d3e565318f95
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810063"
---
# <a name="troubleshoot-your-firewall-in-windows-server-essentials"></a>Solucionar problemas do firewall no Windows Server Essentials

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Se você tiver problemas com o acesso remoto, execute o assistente Reparar Acesso em Qualquer Local.

### <a name="to-run-the-repair-anywhere-access-wizard"></a>Para executar o assistente Reparar Acesso em Qualquer Local

1. Abra o Painel.

2. Clique em **Configurações**, clique na guia **Acesso em Qualquer Local** e clique em **Reparar**.

3. Siga as instruções no assistente Reparar Acesso em Qualquer Local.

   Se você estiver usando uma configuração de rede avançada ou um firewall não Microsoft, talvez seja necessário abrir portas adicionais no firewall. As portas na tabela a seguir são registradas na IANA (Internet Assigned Numbers Authority).

|Número da porta|Descrição|
|-----------------|-----------------|
|65500|Serviço Web de certificado|
|65510 e 65515|Site de implantação do computador cliente|
|65520|Serviço Web para computadores cliente Mac|
|65532|Estrutura do provedor para comunicações loopback do servidor|
|6602|Estrutura do provedor para a comunicação entre os computadores cliente e servidor|

## <a name="see-also"></a>Consulte também

-   [Usar o Acesso via Web Remoto](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Gerenciar o Acesso via Web Remoto](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Gerenciar o Acesso em Qualquer Local](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Gerenciar o Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)

-   [Suporte ao Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

