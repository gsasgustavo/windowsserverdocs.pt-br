---
title: Etapas para configurar o laboratório de teste com autenticação OTP e RSA SecurID
description: Este tópico faz parte do guia de laboratório de teste – demonstre o DirectAccess com autenticação OTP e RSA SecurID para Windows Server 2016
manager: brianlic
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 5ed481a474203e9436796ffa87a30c41ac9fa1cd
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949782"
---
# <a name="steps-for-configuring-the-test-lab-with-otp-authentication-and-rsa-securid"></a>Etapas para configurar o laboratório de teste com autenticação OTP e RSA SecurID

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

As etapas a seguir descrevem como configurar a infraestrutura de acesso remoto, configurar o servidor de acesso remoto e o cliente e testar a conectividade do DirectAccess nas sub-redes HomeNet e Internet.

Neste guia de laboratório de teste, você criará um acesso remoto com o ambiente de OTP executando as seguintes etapas:

-   [Etapa 1: concluir a configuração do DirectAccess](assetId:///4dbf877f-02fb-439b-907a-f5b3f1d8afa6). Conclua todas as etapas no [Guia de laboratório de teste: demonstre a configuração do servidor único do DirectAccess com IPv4 e IPv6 mistos](https://go.microsoft.com/fwlink/p/?LinkId=237004).

-   [Etapa 2: configurar o App1](assetId:///c1bb590f-91d4-4ed5-bceb-b0e36eabd4ff). Configure o APP1 com modelos de certificado de OTP para uso pelo EDGE1.

-   [Etapa 3: configurar DC1](assetId:///904a6edc-a771-45ed-9630-a34a680bb522). Verifique o nome principal do usuário definido em DC1.

-   [Etapa 7: instalar e configurar o RSA](assetId:///baa4c28c-add7-42e2-8afd-ccc7a559406a). Instale e configure o RSA, um servidor RADIUS e de OTP e configure o EDGE1 para OTP.

-   [Etapa 11: verificar a integridade da OTP em EDGE1](assetId:///3b397a4a-8478-47f2-a932-9e8e048c14ba). Verifique se o status de OTP está íntegro no servidor de acesso remoto.

-   [Etapa 8: testar a conectividade do DirectAccess da sub-rede HomeNet](assetId:///ba1652a6-0692-4add-91ca-34a84956ba14). Testar a funcionalidade de OTP do DirectAccess por trás de um dispositivo NAT.

-   [Etapa 10: testar a conectividade do DirectAccess da Internet](assetId:///321149eb-5f23-4a0b-b8fb-1244540126e9). Testar a conectividade de cliente do DirectAccess da Internet.

-   [Etapa 12: instantâneo da configuração](assetId:///8a51ed3c-9c32-402f-85d1-617ce46845b4). Depois de concluir o laboratório de teste, tire um instantâneo do DirectAccess em funcionamento com a configuração de OTP para que você possa retornar a ele mais tarde para testar cenários adicionais.



