---
title: VPN (rede virtual privada)
description: Saiba como você pode usar o gateway RAS como um servidor VPN de locatário único.
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 3e5f8a6a68fc62bb6be02a6a332547c8d301aa95
ms.sourcegitcommit: decb6c8caf4851b13af271d926c650d010a6b9e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98177245"
---
# <a name="virtual-private-networking-vpn"></a>VPN (rede virtual privada)

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016, Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>Gateway RAS como um servidor VPN de locatário único

No Windows Server 2016, a função de servidor de acesso remoto é um agrupamento lógico das tecnologias de acesso à rede relacionadas a seguir.

- Serviço de acesso remoto (RAS)
- Roteamento
- Proxy de aplicativo Web

Essas tecnologias são os serviços de função da função do servidor de acesso remoto.

Ao instalar a função de servidor de acesso remoto com o assistente para adicionar funções e recursos ou o Windows PowerShell, você pode instalar um ou mais desses três serviços de função.

Ao instalar o serviço de função **DirectAccess e VPN (RAS)** , você está implantando o gateway de serviço de acesso remoto (**Gateway de Ras**). Você pode implantar o gateway RAS como um servidor de rede virtual privada (VPN) de gateway de RAS de locatário único que fornece muitos recursos avançados e funcionalidade aprimorada.

>[!NOTE]
>Você também pode implantar o gateway RAS como um servidor VPN multilocatário para uso com o SDN (rede definida pelo software) ou como um servidor DirectAccess. Para obter mais informações, consulte [Gateway de Ras](../ras-gateway/ras-gateway.md), [rede definida por software (SDN)](../../../networking/sdn/software-defined-networking.md)e [DirectAccess](../directaccess/directaccess.md).

## <a name="related-topics"></a>Tópicos relacionados
- [Always on recursos e funcionalidades de VPN](vpn-map-da.md): neste tópico, você aprende sobre os recursos e a funcionalidade de Always on VPN.

- [Configurar túneis de dispositivo VPN no Windows 10](vpn-device-tunnel-config.md): Always on VPN oferece a capacidade de criar um perfil VPN dedicado para o dispositivo ou computador. Always On conexões VPN incluem dois tipos de túneis: _túnel de dispositivo_ e túnel de _usuário_. O túnel de dispositivo é usado para cenários de conectividade pré-login e para fins de gerenciamento de dispositivos. O túnel do usuário permite que os usuários acessem recursos da organização por meio de servidores VPN.

- [Always on implantação de VPN para Windows Server 2016 e Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md): fornece instruções sobre como implantar o acesso remoto como um gateway de Ras VPN de locatário único para conexões VPN ponto a site que permitem que seus funcionários remotos se conectem à rede da sua organização com conexões VPN Always on. É recomendável revisar os guias de design e implantação para cada uma das tecnologias usadas nesta implantação.

- [Guia técnico de VPN do Windows 10](/windows/access-protection/vpn/vpn-guide): orienta você pelas decisões que você fará para clientes do Windows 10 em sua solução de VPN corporativa e como configurar sua implantação. Você pode encontrar referências ao provedor de serviços de configuração do VPNv2 (CSP) e fornece instruções de configuração de MDM (gerenciamento de dispositivo móvel) usando Microsoft Intune e o modelo de perfil VPN para Windows 10.

- [Como criar perfis VPN no Configuration Manager](/configmgr/protect/deploy-use/create-vpn-profiles): neste tópico, você aprende a criar perfis vpn no Configuration Manager.

- [Configurar conexões VPN Always on cliente do Windows 10](./always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md): Este tópico descreve as opções e o esquema do ProfileXML e como criar a VPN ProfileXML. Depois de configurar a infraestrutura do servidor, você deve configurar os computadores cliente do Windows 10 para se comunicar com essa infraestrutura com uma conexão VPN.

- [Opções de perfil VPN](/windows/access-protection/vpn/vpn-profile-options): Este tópico descreve as configurações de perfil VPN no Windows 10 e saiba como configurar perfis VPN usando o Intune ou Configuration Manager. Você pode definir todas as configurações de VPN no Windows 10 usando o nó ProfileXML no CSP VPNv2.
