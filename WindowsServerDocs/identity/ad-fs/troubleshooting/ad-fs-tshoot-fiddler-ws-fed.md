---
title: Solução de problemas AD FS-Fiddler-WS-Federation
description: Este documento mostra um rastreamento detalhado de um WS-Federation Exchange com AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/18/2018
ms.topic: article
ms.openlocfilehash: 96d202a0c4379d2d52e41bdfb0c750e0e64ffaf2
ms.sourcegitcommit: 6717decb5839aa340c81811d6fde020aabaddb3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98781920"
---
# <a name="ad-fs-troubleshooting---fiddler---ws-federation"></a>Solução de problemas AD FS-Fiddler-WS-Federation

![Diagrama de Federação do AD FS e do Windows Server](media/ad-fs-tshoot-fiddler-ws-fed/fiddler9.png)

## <a name="step-1-and-2"></a>Etapa 1 e 2

Este é o início do nosso rastreamento.  Neste quadro, vemos o seguinte:

![Início do rastreamento do Fiddler](media/ad-fs-tshoot-fiddler-ws-fed/fiddler1.png)

Solicitação:

- HTTP GET para nossa terceira parte confiável (http://sql1.contoso.com/SampApp)

Resposta:

- A resposta é um HTTP 302 (redirecionamento).  Os dados de transporte no cabeçalho de resposta mostram para onde redirecionar (https://sts.contoso.com/adfs/ls)
- A URL de redirecionamento contém wa = wsignin 1,0, que nos informa que nosso aplicativo RP criou um WS-Federation solicitação de entrada para nós e o enviou para o ponto de extremidade/adfs/ls/do AD FS.  Isso é conhecido como associação de redirecionamento.

![Dados de transporte no cabeçalho de resposta](media/ad-fs-tshoot-fiddler-ws-fed/fiddler2.png)

## <a name="step-3-and-4"></a>Etapa 3 e 4

![Rastreamento Fiddler de continuação](media/ad-fs-tshoot-fiddler-ws-fed/fiddler3.png)

Solicitação:

- HTTP GET para nosso servidor de AD FS (STS. contoso. com)

Resposta:

- A resposta é um prompt para credenciais.  Isso indica que estamos usando a autenticação de formulários
- Ao clicar no WebView da resposta, você poderá ver o prompt de credenciais.

![Captura de tela da exibição da Web da resposta mostrando o prompt de credenciais.](media/ad-fs-tshoot-fiddler-ws-fed/fiddler6.png)

## <a name="step-5-and-6"></a>Etapa 5 e 6

![Guia do WebView da tela de prompt de solicitação de credenciais](media/ad-fs-tshoot-fiddler-ws-fed/fiddler4.png)

Solicitação:

- HTTP POST com nosso nome de usuário e senha.
- Apresentamos nossas credenciais.  Examinando os dados brutos na solicitação, podemos ver as credenciais

Resposta:

- A resposta é encontrada e o cookie criptografado MSIAuth é criado e retornado.  Isso é usado para validar a declaração SAML produzida por nosso cliente.  Isso também é conhecido como "cookie de autenticação" e só estará presente quando AD FS for o IDP.

## <a name="step-7-and-8"></a>Etapa 7 e 8

![Captura de tela do rastreamento Fiddler que mostra a solicitação H T T P Get e a resposta a essa solicitação.](media/ad-fs-tshoot-fiddler-ws-fed/fiddler5.png)

Solicitação:

- Agora que autenticamos, fazemos outro HTTP GET para o servidor de AD FS e apresentamos nosso token de autenticação

Resposta:

- A resposta é um HTTP OK, o que significa que AD FS autenticou o usuário com base nas credenciais fornecidas
- Além disso, definimos 3 cookies de volta para o cliente
    - MSISAuthenticated contém um valor de carimbo de data/hora codificado em base64 para quando o cliente foi autenticado.
    - MSISLoopDetectionCookie é usado pelo mecanismo de detecção de loop infinito AD FS para interromper os clientes que acabaram em um loop de redirecionamento infinito para o servidor de Federação. Os dados do cookie são um carimbo de data/hora codificado em base64.
    - MSISSignout é usado para acompanhar o IdP e todos os RPs visitados para a sessão de SSO. Esse cookie é utilizado quando uma saída de WS-Federation é invocada. Você pode ver o conteúdo desse cookie usando um decodificador base64.

## <a name="step-9-and-10"></a>Etapa 9 e 10

![Captura de tela do rastreamento Fiddler mostrando a solicitação H T T P Post e a resposta a essa solicitação.](media/ad-fs-tshoot-fiddler-ws-fed/fiddler7.png)

Solicitação:

- HTTP POST

Resposta:

- A resposta foi encontrada

## <a name="step-11-and-12"></a>Etapa 11 e 12

![Finalização do rastreamento Fiddler](media/ad-fs-tshoot-fiddler-ws-fed/fiddler8.png)

Solicitação:

- HTTP GET

Resposta:

- A resposta está OK

## <a name="next-steps"></a>Próximas etapas

- [Solução de problemas do AD FS](ad-fs-tshoot-overview.md)