---
title: Implantar o modo Cache Hospedado do BranchCache
description: Saiba como criar na rede principal fornecendo instruções para implantar o BranchCache no modo de cache hospedado em uma ou mais filiais com um controlador de domínio Read-Only em que os computadores cliente estão executando o Windows 10, o Windows 8.1 ou o Windows 8 e ingressaram no domínio.
manager: brianlic
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 51d8b27d77ccc47d4d7ad1a460da88f6be8339b9
ms.sourcegitcommit: 605a9b46b74b2c7a9116e631e902467ea02a6e70
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97965618"
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>Implantar o modo Cache Hospedado do BranchCache

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

O guia de rede do Windows Server 2016 core fornece instruções para planejar e implantar os componentes principais necessários para uma rede totalmente funcional e um novo &reg; domínio Active Directory em uma nova floresta.

Este guia explica como criar a rede principal fornecendo instruções para a implantação do BranchCache no modo de cache hospedado em uma ou mais filiais com um controlador de \- domínio somente leitura em que os computadores cliente estão executando o Windows &reg; 10, Windows 8.1 ou Windows 8 e ingressaram no domínio.

>[!IMPORTANT]
>Não use este guia se você estiver planejando implantar ou já tiver implantado um servidor de cache hospedado do BranchCache que esteja executando o Windows Server 2008 R2. Este guia fornece instruções para implantar o modo de cache hospedado com um servidor de cache hospedado que está executando o Windows Server &reg; 2016, o Windows server 2012 R2 ou o Windows server 2012.

Este guia contém as seções a seguir.

- [Pré-requisitos para usar este guia](#bkmk_pre)

- [Sobre este guia](#bkmk_about)

- [O que este guia não contém](#bkmk_not)

- [Visões gerais da tecnologia](#bkmk_tech)

- [Visão geral da implantação do modo de cache hospedado do BranchCache](2-Bc-Hcm-Deploy-Overview.md)

- [Planejamento de implantação do modo de cache hospedado do BranchCache](3-Bc-Hcm-Plan.md)

- [Implantação do modo de cache hospedado do BranchCache](4-Bc-Hcm-Deployment.md)

- [Recursos adicionais](11-Bc-Hcm-additional-resources.md)

## <a name="prerequisites-for-using-this-guide"></a><a name="bkmk_pre"></a>Pré-requisitos para usar este guia

Este é um guia complementar para o guia de rede do Windows Server 2016 Core. Para implantar o BranchCache no modo de cache hospedado com este guia, você deve primeiro fazer o seguinte.

- Implantar uma rede principal em seu escritório principal usando o Guia da rede principal, ou já ter as tecnologias fornecidas no Guia da rede principal instaladas e funcionando corretamente em sua rede. Essas tecnologias incluem TCP \/ IP V4, DHCP, Active Directory Domain Services \( AD DS \) e DNS.

    > [!NOTE]
    > O [Guia de rede](../../core-network-guide.md) do windows Server 2016 Core está disponível na biblioteca técnica do windows Server 2016.

- Implante servidores de conteúdo do BranchCache que estejam executando o Windows Server 2016, o Windows Server 2012 R2 ou o Windows Server 2012 em seu escritório principal ou em uma nuvem data center. Para obter informações sobre como implantar servidores de conteúdo do BranchCache, consulte [recursos adicionais](11-Bc-Hcm-additional-resources.md).

- Estabeleça conexões WAN de rede de longa distância \( \) entre sua filial, seu escritório principal e, se apropriado, seus recursos de nuvem, usando uma VPN de rede virtual privada \( , o \) DirectAccess ou outro método de conexão.

- Implante computadores cliente em sua filial que executam um dos sistemas operacionais a seguir, que fornecem ao BranchCache suporte para Serviço de Transferência Inteligente em Segundo Plano (BITS), protocolo HTTP e SMB (bloco de mensagens de servidor).
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - O Windows 8 Enterprise

> [!NOTE]
> Nos sistemas operacionais a seguir, o BranchCache não dá suporte à funcionalidade HTTP e SMB, mas dá suporte à funcionalidade de BITS do BranchCache.
>     - Windows 10 pro, somente suporte a BITS
>     - Windows 8.1 Pro, somente suporte a BITS
>     - Windows 8 Pro, somente suporte a BITS

## <a name="about-this-guide"></a><a name="bkmk_about"></a>Sobre este guia

Este guia foi projetado para administradores de rede e de sistema que seguiram as instruções no guia de rede do Windows Server 2016 core ou no guia de rede do Windows Server 2012 Core para implantar uma rede principal, ou para aqueles que implantaram anteriormente as tecnologias incluídas no guia de rede principal, incluindo Active Directory Domain Services \( AD DS \) , DNS do serviço \( de nome de domínio \) , DHCP do protocolo de configuração de host dinâmico \( \) e TCP \/

É recomendável que você examine os guias de design e implantação de cada uma das tecnologias usadas neste cenário de implantação. Esses guias podem ajudar a determinar se o cenário de implantação fornece os serviços e as configurações que você precisa para a rede de sua organização.

## <a name="what-this-guide-does-not-provide"></a><a name="bkmk_not"></a>O que este guia não contém

Este guia não fornece informações conceituais sobre o BranchCache, incluindo informações sobre recursos e modos do BranchCache.

Este guia não fornece informações sobre como implantar conexões WAN ou outras tecnologias de filial, como DHCP, um RODC ou um servidor VPN.

Além disso, este guia não fornece orientação sobre o hardware que você deve usar ao implantar um servidor de cache hospedado. É possível executar outros serviços e aplicativos no seu servidor de cache hospedado. No entanto, você deve determinar, com base na carga de trabalho, nos recursos de hardware e no tamanho da filial, se quer instalar o servidor de cache hospedado do BranchCache em determinado computador e quanto espaço em disco alocar para o cache.
Este guia não fornece instruções para configurar computadores que executam o Windows 7. Se você tiver computadores cliente que executam o Windows 7 em suas filiais, você deve configurá-los usando procedimentos diferentes daqueles fornecidos neste guia para computadores cliente que executam o Windows 10, Windows 8.1 e Windows 8.

Além disso, se você tiver computadores que executam o Windows 7, deverá configurar o servidor de cache hospedado com um certificado de servidor emitido por uma autoridade de certificação que os computadores cliente confiam. \(Se todos os seus computadores cliente estiverem executando o Windows 10, Windows 8.1 ou o Windows 8, você não precisará configurar o servidor de cache hospedado com um certificado de servidor.\)
> [!IMPORTANT]
> Se os servidores de cache hospedados estiverem executando o Windows Server 2008 R2, use o [Guia de implantação do BranchCache](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649232(v=ws.10)) do windows Server 2008 R2, em vez deste guia, para implantar o BranchCache no modo de cache hospedado. Aplique as configurações de Política de Grupo que são descritas nesse guia para todos os clientes do BranchCache que estão executando versões do Windows do Windows 7 para o Windows 10. Os computadores que executam o Windows Server 2008 R2 não podem ser configurados usando as etapas deste guia.

## <a name="technology-overviews"></a><a name="bkmk_tech"></a>Visões gerais da tecnologia

Para este guia complementar, o BranchCache é a única tecnologia que você precisa instalar e configurar. Você deve executar comandos de BranchCache do Windows PowerShell nos servidores de conteúdo, como servidores Web e de arquivos, porém você não precisa alterar nem reconfigurar os servidores de conteúdo de qualquer outra forma. Além disso, você deve configurar computadores cliente usando Política de Grupo em seus controladores de domínio que estão executando o AD DS no Windows Server 2016, Windows Server 2012 R2 ou Windows Server 2012.

### <a name="branchcache"></a>BranchCache

O BranchCache é uma tecnologia de otimização de largura de banda de WAN (rede de longa distância) incluída em algumas edições dos sistemas operacionais Windows Server 2016 e Windows 10, bem como em algumas edições do Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2 e Windows 7.

Para otimizar a largura de banda WAN quando os usuários acessam o conteúdo em servidores remotos, o BranchCache baixa o conteúdo solicitado pelo cliente do seu escritório principal ou de seus servidores de conteúdo de nuvem hospedado e armazena em cache o conteúdo em locais de filiais, permitindo que outros computadores cliente em filiais acessem o mesmo conteúdo localmente, e não pela WAN.

Quando você implanta o BranchCache no modo de cache hospedado, deve configurar computadores cliente na filial como clientes do modo de cache hospedado e, em seguida, implantar um servidor de cache hospedado na filial. Este guia demonstra como implantar o servidor de cache hospedado com conteúdo de hash e pré-carregado de seus \- servidores de conteúdo baseados em servidor de arquivos e Web.

### <a name="group-policy"></a>Política de Grupo

Política de Grupo no Windows Server 2016, no Windows Server 2012 R2 e no Windows Server 2012 é uma infraestrutura usada para fornecer e aplicar uma ou mais configurações ou definições de política desejadas a um conjunto de usuários e computadores de destino em um ambiente de Active Directory.

Essa infraestrutura consiste em um mecanismo de Política de Grupo e várias \- extensões do lado do cliente \( CSEs \) que são responsáveis por ler as configurações de política nos computadores cliente de destino.

A Política de Grupo é usada neste cenário para configurar computadores cliente membros do domínio com modo de cache hospedado do BranchCache.

Para continuar com este guia, consulte [visão geral da implantação do modo de cache hospedado do BranchCache](2-Bc-Hcm-Deploy-Overview.md).