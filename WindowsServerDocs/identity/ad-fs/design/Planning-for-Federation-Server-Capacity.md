---
description: 'Saiba mais sobre: planejando a capacidade do servidor de Federação'
ms.assetid: 7013fc21-9ced-4f9d-9588-cb04d6d60924
title: Planning for Federation Server Capacity (Planejando a capacidade do servidor de federação)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c81c589feb940fb686aa865c8368f126ab20562d
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044634"
---
# <a name="planning-for-federation-server-capacity"></a>Planning for Federation Server Capacity (Planejando a capacidade do servidor de federação)

O planejamento de capacidade para servidores de Federação ajuda a estimar:

-   Quais fatores crescem o tamanho do banco de dados de configuração do AD FS.

-   Os requisitos de hardware apropriados para cada servidor de Federação.

-   O número de servidores de Federação a serem colocados em cada organização.

Os servidores de Federação emitem tokens de segurança para usuários. Esses tokens são apresentados a uma terceira parte confiável para consumo. Os servidores de Federação emitem tokens de segurança depois de autenticar um usuário ou depois de receber um token de segurança emitido anteriormente por um parceiro Serviço de Federação. Um token de segurança é solicitado de um Serviço de Federação quando os usuários entram inicialmente em aplicativos federados ou quando seus tokens de segurança expiram enquanto estão acessando aplicativos federados.

Os servidores de Federação são projetados para acomodar configurações de farm de servidor de alta \- disponibilidade que usam a tecnologia NLB de balanceamento de carga de rede da Microsoft \( \) . Os servidores de Federação em uma configuração de farm podem atender solicitações de forma independente, sem acessar nenhum componente de farm comum para cada solicitação. Portanto, há pouca sobrecarga envolvida na expansão de uma implantação de servidor de Federação.

**Recommendations**

-   Para \- implantações de missão crítica ou de alta \- disponibilidade, recomendamos que você crie um farm de servidores de Federação pequeno em cada organização parceira, com pelo menos dois servidores de Federação por farm, para fornecer tolerância a falhas.

-   Com a necessidade de alta disponibilidade e a facilidade de escalar servidores de Federação, escalar horizontalmente é o método recomendado para lidar com números altos de solicitações por segundo para um determinado Serviço de Federação. A expansão para cima além da configuração básica neste guia é improvável de produzir ganhos de manipulação de capacidade significativos.

## <a name="ad-fs-configuration-database-size-and-growth"></a>Tamanho e crescimento do banco de dados de configuração AD FS
O tamanho do banco de dados de configuração de AD FS geralmente é considerado pequeno, e o tamanho do banco de dados não tende a ser uma consideração importante em implantações de AD FS.  O tamanho preciso do banco de dados de configuração do AD FS pode depender muito do número de relações de confiança e dos metadados relacionados à confiança associados, como \- declarações, regras de declaração e configurações de monitoramento configuradas para cada relação de confiança. À medida que o número de entradas de confiança no banco de dados de configuração cresce, a necessidade de mais espaço em disco.

Para obter informações adicionais de implantação sobre o banco de dados de configuração do AD FS, consulte [AD FS considerações sobre topologia de implantação](AD-FS-Deployment-Topology-Considerations.md).

## <a name="memory-cpu-and-disk-space-requirements"></a>Requisitos de memória, CPU e espaço em disco
Felizmente, os requisitos de memória, CPU e espaço em disco para servidores de Federação são modestos e, provavelmente, não são um fator determinante em decisões de hardware. Para obter mais informações sobre os requisitos de hardware, consulte [o apêndice A: revisando requisitos de AD FS](Appendix-A--Reviewing-AD-FS-Requirements.md).

> [!NOTE]
> Em testes que foram executados pela equipe de produto AD FS usando um farm de servidores de Federação configurado com um SQL Server dedicado para armazenar o banco de dados de configuração do AD FS, a carga geral no SQL Server tendiam para ser baixa. Em um teste usando um \- farm de servidores de Federação \- que foi configurado para usar um único SQL Server, a utilização da CPU não excedeu 10%, apesar dos testes que trouxeram os servidores de Federação para a utilização de destino.

## <a name="estimate-the-number-of-federation-servers-for-your-organization"></a><a name="bk_estimatefs"></a>Estimar o número de servidores de federação da sua organização
Em um esforço para simplificar o processo de planejamento de hardware para servidores de Federação, a equipe de produto AD FS desenvolveu a planilha de dimensionamento de planejamento de capacidade AD FS. Esta planilha do Excel inclui a calculadora, \- como a funcionalidade que obterá os dados de uso esperados que você fornece sobre os usuários em sua organização e retorna um número ideal de servidores de Federação recomendados para seu ambiente de produção AD FS.

> [!NOTE]
> O número de servidores de Federação que essa planilha recomendará é baseado nas especificações de hardware e rede que a equipe de produto AD FS usada durante o teste. Portanto, o número de servidores de Federação que a planilha recomendará deve ser compreendido nesse contexto.  Para obter mais informações sobre as especificações usadas durante o teste, consulte o tópico intitulada [planejando a capacidade do AD FS Server](Planning-for-AD-FS-Server-Capacity.md).

### <a name="using-the-ad-fs-capacity-planning-sizing-spreadsheet"></a>Usando a planilha de dimensionamento de planejamento de capacidade AD FS
Ao usar essa planilha, você precisará selecionar um valor \( de **40%**, **60%** ou **80%** \) que melhor represente o percentual do total de usuários que você espera enviar solicitações de autenticação para seus servidores de Federação durante períodos de pico de uso.

Em seguida, você precisará selecionar um valor \( de **1 minuto**, **15 minutos** ou uma **hora** \) que melhor represente a duração do período de pico de uso até o último. Por exemplo, você pode estimar 40% como o valor do número total de usuários que efetuarão logon dentro de um período de 15 minutos ou que 60% dos usuários entrarão em um período de 1 hora. Juntos, esses valores definem o perfil de carga de pico pelo qual sua recomendação de dimensionamento será calculada.

Em seguida, você precisará especificar o número total de usuários que exigirão acesso de logon único \- ao aplicativo de reconhecimento de declarações de destino \- , com base em se os usuários são:

-   Logon em Active Directory de um computador local conectado fisicamente à sua rede corporativa \( por meio da autenticação integrada do Windows\)

-   Fazer logon no Active Directory remotamente de um computador que não está conectado fisicamente à sua rede corporativa \( por meio da autenticação integrada do Windows ou nome de usuário e senha\)

-   De outra organização e está tentando acessar o aplicativo de reconhecimento de declarações \- de destino de um parceiro confiável

-   De um provedor de identidade SAML 2,0 e está tentando acessar o aplicativo de reconhecimento de declarações de destino \-

#### <a name="how-to-use-this-spreadsheet"></a>Como usar esta planilha
Você pode usar as etapas a seguir para cada instância de farm de servidores de Federação que planeja implantar para determinar o número recomendado de servidores de Federação.

1.  Baixe e abra a [planilha de dimensionamento de planejamento de capacidade AD FS para o Windows server 2012 R2](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx) ou a [planilha de dimensionamento de planejamento de capacidade AD FS para o Windows Server 2016](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx).

2.  Na célula à direita do **período de uso do sistema de pico, espero que esse percentual dos meus usuários autentiquem** a célula, clique na célula e use as setas suspensas \- para selecionar o nível de utilização estimado do sistema, **40%**, **60%** ou **80%** para a implantação.

3.  Na célula à direita do **período de tempo seguinte** , clique na célula e, em seguida, use as setas suspensas \- para selecionar **1 minuto**, **15 minutos** ou **1 hora** para selecionar a duração da carga de pico.

4.  Na célula à direita da célula **Inserir número estimado de aplicativos internos \( , como SharePoint \( 2007 ou 2010 \) ou aplicativos \) Web com reconhecimento de declarações** , digite o número de aplicativos internos que você usará em sua organização.

5.  Na célula à direita do **Inserir número estimado de aplicativos online, como o \( Office 365 Exchange Online, SharePoint Online ou a célula do \) Lync Online** , digite o número de aplicativos ou serviços online que você usará em sua organização.

6.  Sob a célula intitulada **número de usuários**, digite um número em cada linha que se aplica a um cenário de aplicativo de exemplo aos quais os usuários precisarão de acesso de logon único \- . Essa coluna deve conter o número de usuários definidos, e não os usuários de pico por segundo. Se as tentativas de acesso feitas ao aplicativo precisarem primeiro passar pela página de descoberta de realm inicial, digite **Y**. Se você não tiver certeza dessa seleção, digite **Y**.

7.  Examine os seguintes valores recomendados que são fornecidos:

    1.  Para o número total de servidores de Federação recomendados, consulte a célula inferior direita que é realçada em cinza.

    2.  Para o número de servidores recomendados para cada cenário de aplicativo de exemplo, consulte a célula na linha realçada em cinza.

> [!NOTE]
> O valor que será calculado automaticamente na célula à direita da célula intitulada **número total de servidores de Federação recomendados** na parte inferior da planilha contém uma fórmula que adicionará um buffer adicional de 20% ao total da soma de todos os valores em cada uma das linhas individuais que o antecedem. A fórmula adicionada ao **número total de servidores de Federação recomendados** compilações de célula nesse buffer para o número total recomendado de servidores de Federação implantados para tornar muito improvável que a carga geral no farm sempre atingirá seu ponto de saturação.

## <a name="see-also"></a>Consulte Também
[Guia de design do AD FS no Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
