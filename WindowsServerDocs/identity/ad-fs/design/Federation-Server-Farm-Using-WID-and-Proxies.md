---
description: 'Saiba mais sobre: farm de servidores de Federação AD FS herdados usando WID e proxies'
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: Farm de servidores de federação usando WID e proxies
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 186c75d6ec7660258f8b16b93e5d35bb74669ec2
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97046904"
---
# <a name="legacy-ad-fs-federation-server-farm-using-wid-and-proxies"></a>Farm de servidores de Federação AD FS herdados usando WID e proxies

Essa topologia de implantação para Serviços de Federação do Active Directory (AD FS) (AD FS) é idêntica ao farm de servidores de Federação com a topologia do banco de dados interno do Windows (WID), mas adiciona computadores proxy à rede de perímetro para dar suporte a usuários externos. Esses proxies redirecionam as solicitações de autenticação de cliente que vêm de fora de sua rede corporativa para o farm de servidores de Federação. Nas versões anteriores do AD FS, esses proxies eram chamados de proxies de servidor de Federação.

> [!IMPORTANT]
> No Serviços de Federação do Active Directory (AD FS) (AD FS) no Windows Server 2012 R2, a função de um proxy de servidor de Federação é tratada por um novo serviço de função de acesso remoto chamado proxy de aplicativo Web. Para habilitar sua AD FS para acessibilidade de fora da rede corporativa, que foi a finalidade de implantar um proxy de servidor de Federação em versões herdadas do AD FS, como AD FS 2,0 e AD FS no Windows Server 2012, você pode implantar um ou mais proxies de aplicativo Web para AD FS no Windows Server 2012 R2.
>
> No contexto de AD FS, o proxy de aplicativo Web funciona como um proxy de servidor de Federação AD FS. Além disso, o Proxy de Aplicativo Web fornece funcionalidade de proxy reverso para aplicativos Web dentro da rede corporativa. Isso permite aos usuários acessá-los de qualquer dispositivo fora da rede corporativa. Para obter mais informações sobre o serviço da função Proxy de Aplicativo Web, consulte Visão geral de proxy de aplicativo Web.
>
> Para planejar a implantação do proxy de Aplicativo Web, é possível examinar as informações nos tópicos a seguir:
>
> - [Planejar a WAP (infraestrutura de proxy de aplicativo Web)](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))
> - [planejar o Servidor Proxy de Aplicativo Web](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))

## <a name="deployment-considerations"></a>Considerações de implantação
Esta seção descreve as várias considerações sobre o público-alvo, os benefícios e as limitações associados a essa topologia de implantação.

### <a name="who-should-use-this-topology"></a>Quem deve usar essa topologia?

- Organizações com 100 ou menos relações de confiança configuradas que precisam fornecer os usuários internos e usuários externos (que estão conectados a computadores que estão localizados fisicamente fora da rede corporativa) com acesso de logon único (SSO) a aplicativos ou serviços federados

- Organizações que precisam fornecer os usuários internos e usuários externos com acesso de SSO a Microsoft Office 365

- Organizações menores que têm usuários externos e exigem serviços redundantes e escalonáveis

### <a name="what-are-the-benefits-of-using-this-topology"></a>Quais são os benefícios de usar essa topologia?

- Os mesmos benefícios listados para o [farm de servidores de Federação usando](Federation-Server-Farm-Using-WID.md) a topologia wid, além do benefício de fornecer acesso adicional para usuários externos

### <a name="what-are-the-limitations-of-using-this-topology"></a>Quais são as limitações do uso dessa topologia?

- As mesmas limitações listadas para o [farm de servidores de Federação usando](Federation-Server-Farm-Using-WID.md) a topologia wid

    | 1 a 100 relações de confiança de RP | Mais de 100 relações de confiança de RP |
    |--|--|
    | **1 a 30 nós do AD FS:** Suporte ao WID | **1 a 30 nós do AD FS:** Sem suporte para uso do WID – O SQL é exigido |
    | **Mais de 30 Nós do AD FS:** Sem suporte para uso do WID – O SQL é exigido | **Mais de 30 Nós do AD FS:** Sem suporte para uso do WID – O SQL é exigido |

## <a name="server-placement-and-network-layout-recommendations"></a>Recomendações de layout de rede e posicionamento do servidor
Para implantar essa topologia, além de adicionar dois proxies de aplicativo Web, você deve verificar se a rede de perímetro também pode fornecer acesso a um servidor DNS (sistema de nomes de domínio) e a um segundo host NLB (balanceamento de carga de rede). O segundo host NLB deve ser configurado com um cluster NLB que usa um endereço IP de cluster acessível pela Internet e deve usar a mesma configuração de nome DNS do cluster que o cluster NLB anterior que você configurou na rede corporativa (fs.fabrikam.com). Os proxies de aplicativo Web também devem ser configurados com endereços IP acessíveis pela Internet.

A ilustração a seguir mostra o farm de servidores de Federação existente com a topologia WID que foi descrita anteriormente e como a empresa fictícia Fabrikam, Inc., fornece acesso a um servidor DNS de perímetro, adiciona um segundo host NLB com o mesmo nome DNS de cluster (fs.fabrikam.com) e adiciona dois proxies de aplicativo Web (wap1 e WAP2) à rede de perímetro.

![Farm de WID e proxies](media/WIDFarmADFSBlue.gif)

Para obter mais informações sobre como configurar seu ambiente de rede para uso com servidores de Federação ou proxies de aplicativo Web, consulte a seção "requisitos de resolução de nomes" em [AD FS requisitos](AD-FS-Requirements.md) e [planejar a WAP (infraestrutura de proxy de aplicativo Web)](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11)).

## <a name="see-also"></a>Consulte Também
[Planejar sua topologia](Plan-Your-AD-FS-Deployment-Topology.md) 
 de implantação do AD FS [Guia de design de AD FS no Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)

