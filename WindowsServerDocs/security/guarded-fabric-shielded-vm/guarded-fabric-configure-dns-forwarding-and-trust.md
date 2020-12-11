---
description: 'Saiba mais sobre: configurar o encaminhamento de DNS no domínio HGS e uma relação de confiança unidirecional com o domínio de malha'
title: Configurar o encaminhamento DNS e a confiança do domínio
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 2031c7f56c96764a716f29afc4f0cfe27c452646
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97040364"
---
# <a name="configure-dns-forwarding-in-the-hgs-domain-and-a-one-way-trust-with-the-fabric-domain"></a>Configurar o encaminhamento de DNS no domínio HGS e uma relação de confiança unidirecional com o domínio de malha

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

>[!IMPORTANT]
>O modo AD é preterido a partir do Windows Server 2019. Para ambientes em que o atestado do TPM não é possível, configure o [atestado de chave do host](guarded-fabric-initialize-hgs-key-mode.md). O atestado de chave de host fornece garantia semelhante ao modo AD e é mais simples de configurar.

Use as etapas a seguir para configurar o encaminhamento de DNS e estabelecer uma relação de confiança unidirecional com o domínio de malha. Essas etapas permitem que o HGS Localize os controladores de domínio de malha e valide a associação de grupo dos hosts Hyper-V.

1.  Execute o comando a seguir em uma sessão do PowerShell com privilégios elevados para configurar o encaminhamento de DNS. Substitua fabrikam.com pelo nome do domínio de malha e digite os endereços IP dos servidores DNS no domínio de malha. Para maior disponibilidade, aponte para mais de um servidor DNS.

    ```powershell
    Add-DnsServerConditionalForwarderZone -Name "fabrikam.com" -ReplicationScope "Forest" -MasterServers <DNSserverAddress1>, <DNSserverAddress2>
    ```

2.  Para criar uma relação de confiança de floresta unidirecional, execute o seguinte comando em um prompt de comando com privilégios elevados:

    Substitua `bastion.local` pelo nome do domínio HgS e `fabrikam.com` pelo nome do domínio de malha. Forneça a senha para um administrador do domínio de malha.

    ```powershell
    netdom trust bastion.local /domain:fabrikam.com /userD:fabrikam.com\Administrator /passwordD:<password> /add
    ```

## <a name="next-step"></a>Próxima etapa

> [!div class="nextstepaction"]
> [Configurar HTTPS](guarded-fabric-configure-hgs-https.md)
