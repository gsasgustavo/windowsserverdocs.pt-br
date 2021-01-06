---
title: Implantação de certificados de servidor
description: Este tópico faz parte do guia implantar certificados de servidor para implantações com e sem fio 802.1 X
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: c48fb74543ef115d0dc30c9d052bceb5ed390660
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950142"
---
# <a name="server-certificate-deployment"></a>Implantação de certificados de servidor

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Siga estas etapas para instalar uma AC (autoridade de certificação) raiz corporativa e implantar certificados de servidor para uso com PEAP e EAP.

> [!IMPORTANT]
> Antes de instalar Active Directory serviços de certificados, você deve nomear o computador, configurar o computador com um endereço IP estático e ingressar o computador no domínio. Depois de instalar o AD CS, não é possível alterar o nome do computador ou a associação de domínio do computador, no entanto, você pode alterar o endereço IP, se necessário. Para obter mais informações sobre como realizar essas tarefas, consulte o guia de rede do Windows Server &reg; 2016 [Core](../../Core-Network-Guide.md).


-   [Instalar o servidor Web WEB1](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)

-   [Criar um registro de alias (CNAME) em DNS para WEB1](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)

-   [Configurar o WEB1 para distribuir listas de certificados revogados (CRLs)](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)

-   [Preparar o arquivo inf do CAPolicy](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)

-   [Instalar a autoridade de certificação](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)

-   [Configurar as extensões de CDP e AIA no CA1](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)

-   [Copiar o certificado de Autoridade de Certificação e CRL para o diretório virtual](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)

-   [Configurar o modelo de certificado do servidor](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)

-   [Configurar o registro automático de certificados do servidor](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)

-   [Atualizar Política de Grupo](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)

-   [Verificar o registro de servidor de um certificado de servidor](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)

> [!NOTE]
> Os procedimentos deste guia não incluem instruções para os casos em que a caixa de diálogo **Controle de Conta de Usuário** é aberta para solicitar sua permissão para continuar. Caso essa caixa de diálogo seja aberta durante a execução dos procedimentos deste guia e em resposta às suas ações, clique em **Continuar**.



