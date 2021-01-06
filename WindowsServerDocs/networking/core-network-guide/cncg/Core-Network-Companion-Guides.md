---
title: Guias Complementares de Rede Principal
description: Este tópico fornece uma visão geral dos guias complementares para o guia de rede do Windows Server 2016 Core
manager: brianlic
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: ffcfbecfa47c39f0bb6e76a6e34953a2ef9140e7
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950232"
---
# <a name="core-network-companion-guidance"></a>Diretrizes de complementar de rede principal

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Embora o [Guia de rede](../core-network-guide.md) do Windows Server 2016 Core forneça instruções sobre como implantar uma nova &reg; floresta Active Directory com um novo domínio raiz e a infraestrutura de rede de suporte, os guias complementares fornecem a capacidade de adicionar recursos à sua rede.

Cada guia complementar permite cumprir uma meta específica, após a implantação de sua rede principal. Em alguns casos, existem vários guias complementarem que, quando implantados juntos e na ordem correta, permitem realizar objetivos muito complexos de forma medida, econômica e razoável.

Se você implantou sua rede principal e seu domínio do Active Directory antes de encontrar o Guia da Rede Principal, ainda pode usar os Guias Complementares para adicionar recursos à sua rede. Simplesmente use o Guia da Rede Principal como uma lista de pré-requisitos e saiba que, para implantar recursos adicionais com os Guias Complementares, a rede deve atender aos pré-requisitos que são fornecidos pelo Guia da Rede Principal.

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Guia complementar de rede de núcleo: implantar certificados de servidor para implantações com e sem fio 802.1 X

Este guia complementar explica como criar a rede principal implantando certificados de servidor para computadores que estão executando o NPS do servidor de políticas de rede \( \) , RAS do serviço de acesso remoto \( \) ou ambos.

Certificados de servidor são necessários quando você implanta métodos de autenticação com base em certificado com EAP de protocolo de autenticação extensível \( \) e EAP protegido \( \) para autenticação de acesso à rede. A implantação de certificados de servidor com Active Directory serviços \( de certificados AD CS \) para EAP e métodos de autenticação com base em certificado PEAP oferece os seguintes benefícios:

- Associando a identidade do servidor NPS ou RAS a uma chave privada
- Um método seguro e econômico para registrar automaticamente certificados em servidores de NPS e RAS do membro do domínio
- Um método eficiente para o gerenciamento de certificados e autoridades de certificação
- Segurança fornecida por autenticação baseada em certificado
- A capacidade de expandir o uso de certificados para outras finalidades

Para obter instruções sobre como implantar certificados de servidor, consulte [implantar certificados de servidor para implantações com e sem fio 802.1 x](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md).
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>Guia complementar de rede de núcleo: implantar Password-Based acesso sem fio autenticado 802.1 X

Este guia complementar explica como criar a rede principal fornecendo instruções sobre como implantar o Institute of Electrical and Electronics Engineers \( IEEE \) 802.1 x \- autenticado com acesso sem fio IEEE 802,11 usando protocolo de autenticação extensível protegido \ – Microsoft Challenge Handshake Authentication Protocol versão 2 \( PEAP \- MS \- CHAP v2 \) .

O método de autenticação PEAP \- MS \- CHAP v2 requer que os servidores de autenticação que executam o servidor de políticas de rede \( NPS \) apresentem clientes sem fio com um certificado de servidor para provar a identidade do NPS para o cliente, mas a autenticação do usuário não é executada usando um certificado-em vez disso, os usuários fornecem seu nome de usuário e senha de domínio.

Como \- o PEAP MS \- CHAP v2 requer que os usuários forneçam credenciais baseadas em senha em vez de um certificado durante o processo de autenticação, normalmente é mais fácil e menos dispendioso implantar do que EAP \- TLS ou PEAP \- TLS.

Antes de usar este guia para implantar o acesso sem fio com o \- método de autenticação PEAP MS \- CHAP v2, você deve fazer o seguinte:

1. Siga as instruções no guia de rede principal para implantar sua infraestrutura de rede principal ou já ter as tecnologias apresentadas nesse guia implantadas em sua rede.
2. Siga as instruções no guia complementar de rede principal implantar certificados de servidor para implantações 802.1 X com e sem fio, ou já ter as tecnologias apresentadas nesse guia implantadas em sua rede.

Para obter instruções sobre como implantar o acesso sem fio com o PEAP \- MS \- CHAP v2, consulte [implantar Password-Based acesso sem fio autenticado 802.1 x](wireless/a-deploy-8021X-wireless-access.md).

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>Guia complementar de rede de núcleo: implantar o modo de cache hospedado do BranchCache

Este guia complementar explica como implantar o BranchCache no modo de cache hospedado em uma ou mais filiais.

O BranchCache é uma tecnologia de otimização de largura de banda de WAN (rede de longa distância) incluída em algumas edições dos sistemas operacionais Windows Server 2016 e Windows 10, bem como nas versões anteriores do Windows e do Windows Server.

Quando você implanta o BranchCache no modo de cache hospedado, o cache de conteúdo em uma filial é hospedado em um ou mais servidores, que são chamados de servidores de cache hospedado. Os servidores de cache hospedados podem executar cargas de trabalho além de hospedar o cache, o que permite que você use o servidor para várias finalidades na filial.

O modo de cache hospedado do BranchCache aumenta a eficiência do cache porque o conteúdo está disponível mesmo que o cliente que originalmente solicitou e armazene os dados em cache esteja offline. Como o servidor de cache hospedado está sempre disponível, mais conteúdo é armazenado em cache, proporcionando maiores economias de largura de banda de WAN e aumentando a eficiência do BranchCache.

Quando você implanta o modo de cache hospedado, todos os clientes em uma filial de várias sub-redes podem acessar um único cache, que é armazenado no servidor de cache hospedado, mesmo que os clientes estejam em sub-redes diferentes.

Para obter instruções sobre como implantar o BranchCache no modo de cache hospedado, consulte [implantar o modo de cache hospedado do BranchCache](bc-hcm/1-Deploy-Bc-Hcm.md).