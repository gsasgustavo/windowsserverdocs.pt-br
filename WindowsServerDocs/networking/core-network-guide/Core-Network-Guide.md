---
title: Principais componentes de rede
description: Este guia fornece instruções sobre como planejar e implantar os componentes principais necessários para uma rede totalmente funcional e um novo domínio de Active Directory em uma nova floresta com o Windows Server 2016
manager: brianlic
ms.topic: article
ms.assetid: b3cd60f7-d380-4712-9a78-0a8f551e1121
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f746422ee05afc4f000693138c1f2efb3b7f70a9
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96866115"
---
# <a name="core-network-components"></a>Principais componentes de rede

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Este guia fornece instruções sobre como planejar e implantar os componentes principais necessários para uma rede totalmente funcional e um novo domínio de Active Directory em uma nova floresta.

> [!NOTE]
> Este guia está disponível para download no formato do Microsoft Word na galeria do TechNet. Para obter mais informações, consulte [Guia de rede principal do Windows Server 2016](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683).

Este guia contém as seções a seguir.

- [Sobre este guia](#BKMK_about)

- [Visão geral da rede principal](#BKMK_overview)

- [Planejamento da rede principal](#BKMK_planning)

- [Implantação da rede principal](#BKMK_deployment)

- [Recursos técnicos adicionais](#BKMK_resources)

- [Apêndices A a E](#BKMK_appendix)

## <a name="about-this-guide"></a><a name="BKMK_about"></a>Sobre este guia
Este guia se destina aos administradores de rede e de sistema que estão instalando uma nova rede ou que desejam criar uma rede baseada em domínio para substituir uma rede constituída de grupos de trabalho. O cenário de implantação fornecido neste guia é especialmente útil quando você prevê a necessidade de adicionar mais recursos e serviços a sua rede no futuro.

Recomendamos que você leia os guias de design e de implantação para cada uma das tecnologias usadas neste cenário de implantação para ajudar a determinar se este guia fornece os serviços e configurações que você precisa.

Uma rede principal é um conjunto de hardware de rede, dispositivos e software que fornece os serviços fundamentais para as necessidades da TI (tecnologia da informação) de sua organização.

Uma rede principal do Windows Server fornece muitos benefícios, incluindo alguns a seguir.

- Os protocolos principais de conectividade da rede entre computadores e outros dispositivos compatíveis com os protocolos TCP/IP. TCP/IP é um conjunto de protocolos padrão para conexão de computadores e criação de redes. O TCP/IP é um software de protocolo de rede fornecido com os sistemas operacionais Microsoft Windows que implementa e dá suporte ao conjunto de protocolos TCP/IP.

- A atribuição automática de endereços IP do protocolo DHCP para computadores e outros dispositivos que são configurados como clientes DHCP. A configuração manual dos endereços IP em todos os computadores na sua rede é demorado e menos flexível que fornecer dinamicamente computadores e outros dispositivos com as configurações de endereço IP usando um servidor DHCP.

- Serviços de resolução de nomes do DNS (Sistema de Nomes de Domínios) O DNS permite que os usuários, computadores, aplicativos e serviços encontrem os endereços IP dos computadores e dispositivos na rede usando o Nome de Domínio Totalmente Qualificado do computador ou dispositivo.

- Uma floresta, que é um ou mais domínios do Active Directory que compartilham as mesmas definições de classe e de atributo (esquema), informações de local e replicação (configuração) e capacidades de pesquisa da floresta (catálogo global).

- Um domínio raiz de floresta, que é o primeiro domínio criado em uma nova floresta. Os grupos Administradores de Empresa e Administradores de Esquema (que são grupos administrativos em toda a floresta) estão localizados no domínio raiz da floresta. Além disso, um domínio raiz da floresta, tal como acontece com outros domínios, é uma coleção de objetos de computador, de usuário e de grupo que são definidos pelo administrador no AD DS (Serviços de Domínio Active Directory). Esses objetos compartilham um banco de dados de diretório comum e políticas de segurança. Eles também poderão compartilhar relações de segurança com outros domínios se você adicionar domínios à medida que sua organização crescer. O serviço de diretório também armazena os dados de diretório e permite que computadores autorizados, aplicativos e usuários acessem os dados.

- Um banco de dados de contas de usuário e de computador. O serviço de diretório fornece um banco de dados de contas de usuário centralizado que permite que você crie contas de usuário e de computador para pessoas e computadores que estão autorizados a se conectar à sua rede e acessar os recursos da rede, como aplicativos, bancos de dados, arquivos e pastas compartilhados, e impressoras.

Uma rede principal também permite escalar sua rede à medida que sua organização cresce e os requisitos de TI mudam. Por exemplo, com uma rede principal, você pode adicionar domínios, sub-redes IP, serviços de acesso remoto, serviços sem fio e outros recursos e funções de servidor fornecidos pelo Windows Server 2016.

### <a name="network-hardware-requirements"></a>Requisitos de hardware de rede
Para implantar com êxito uma rede principal, implante o hardware de rede, incluindo o seguinte:

- Cabeamento Ethernet, Fast Ethernet ou Gigabyte Ethernet

- Um hub, comutador de Camada 2 ou 3, roteador ou outro dispositivo que executa a função de retransmissão do tráfego de rede entre computadores e dispositivos.

- Os computadores que atendem aos requisitos mínimos de hardware para os sistemas operacionais de cliente e servidor respectivos.

## <a name="what-this-guide-does-not-provide"></a>O que este guia não contém
Este guia não fornece instruções para implantar o seguinte:

- Hardware de rede, como cabeamentos, roteadores, comutadores e hubs

- Recursos de rede adicionais, como impressoras e servidores de arquivos

- Conectividade com a Internet

- Acesso remoto

- Acesso sem fio

- Implantação do computador cliente

> [!NOTE]
> Os computadores que executam sistemas operacionais cliente do Windows são configurados por padrão para receber concessões de endereço IP do servidor DHCP. Portanto, nenhuma configuração adicional do protocolo DHCP ou IPv4 nos computadores clientes é necessária.

## <a name="technology-overviews"></a>Visões gerais de tecnologia
As seções a seguir fornecem visões gerais breves das tecnologias exigidas que são implantadas para criar uma rede principal.

### <a name="active-directory-domain-services"></a>Active Directory Domain Services
Um diretório é uma estrutura hierárquica que armazena informações sobre objetos na rede, como usuários e computadores. Um serviço de diretório, como o AD DS, fornece os métodos para armazenar dados de diretório e disponibilizá-los para administradores e usuários da rede. Por exemplo, o AD DS armazena informações sobre contas de usuário, incluindo nomes, endereços de email, senhas e números de telefone e permite que outros usuários autorizados da mesma rede acessem essas informações.

### <a name="dns"></a>DNS
O DNS é um protocolo de resolução de nomes para redes TCP/IP, como a Internet ou uma rede da organização. Um servidor DNS hospeda as informações que permite que os computadores cliente e serviços resolvam nomes DNS alfanuméricos fáceis de reconhecer para os endereços IP que os computadores usam para comunicação entre si.

### <a name="dhcp"></a>DHCP
O DHCP é um padrão de IP para simplificar o gerenciamento da configuração de IP do host. O padrão DHCP proporciona o uso de servidores DHCP como uma forma de gerenciar a alocação dinâmica de endereços IP e outros detalhes de configuração relacionados para clientes habilitados para DHCP em sua rede.

O DHCP permite que você use um servidor DHCP para atribuir dinamicamente um endereço IP a um computador ou outro dispositivo, como uma impressora em sua rede local. Todos os computadores em uma rede TCP/IP devem ter um endereço IP exclusivo, porque o endereço IP e a máscara de sub-rede relacionada identificam o computador host e a sub-rede à qual o computador está conectado. Usando o DHCP, você pode garantir que todos os computadores configurados como clientes DHCP recebam um endereço IP que seja apropriado para seu local de rede e sua sub-rede e, usando as opções de DHCP (como o gateway padrão e os servidores DNS), você pode fornecer automaticamente aos clientes DHCP as informações que eles precisam para funcionar corretamente na rede.

Para redes baseadas em TCP/IP, o DHCP reduz a complexidade e a quantidade de trabalho administrativo envolvido na reconfiguração dos computadores.

### <a name="tcpip"></a>TCP/IP
O TCP/IP no Windows Server 2016 é o seguinte:

- Software de rede baseado em protocolos de rede padrão do setor.

- Um protocolo de rede de empresa roteável que suporta a conexão de seu computador baseado em Windows com os ambientes LAN (rede de área local) e WAN (rede de longa distância).

- As principais tecnologias e utilitários para conectar seu computador baseado em Windows com os sistemas diferentes com a finalidade de compartilhar informações.

- Uma base para obter acesso aos serviços globais da Internet, como os servidores WWW e FTP.

- Uma estrutura robusta, escalável, multiplataforma, de cliente/servidor.

O TCP/IP oferece utilitários TCP/IP básicos que permitem que computadores baseados no Windows se conectem e compartilhem informações com outros sistemas Microsoft e não Microsoft, incluindo:

-  Windows Server 2016

- Windows 10

-  Windows Server 2012 R2

- Windows 8.1

-  Windows Server 2012

- Windows 8

-  Windows Server 2008 R2

-  Windows 7

-  Windows Server 2008

- Windows Vista

- Hosts da Internet

- Sistemas Apple Macintosh

- Mainframes IBM

- Sistemas UNIX e Linux

- Sistemas VMS abertos

- Impressoras prontas para a rede

- Tablets e telefones celulares com Ethernet com fio ou tecnologia sem fio 802,11 habilitada

## <a name="core-network-overview"></a><a name="BKMK_overview"></a>Visão geral da rede principal
A ilustração a seguir mostra a topologia de Rede Principal do Windows Server.

![Topologia de rede do Windows Server Core](../media/Core-Network-Guide/cng16_overview.jpg)

> [!NOTE]
> Este guia também inclui instruções para adicionar servidores NPS (Servidor de Políticas de Rede) e de Servidor Web (IIS) para sua topologia de rede para fornecer a base para proteger as soluções de acesso à rede, como implantações 802.1X com fio e sem fio que você pode implementar usando guias complementares de Rede Principal. Para obter mais informações, consulte [Implantando recursos opcionais para a autenticação do acesso à rede e dos serviços Web](#BKMK_optionalfeatures).

### <a name="core-network-components"></a>Componentes da rede principal
Estes são os componentes de uma rede principal.

##### <a name="router"></a>Router
Este guia de implantação fornece instruções para a implantação de uma rede principal com duas sub-redes separadas por um roteador que tem o encaminhamento DHCP habilitado. No entanto, você pode implantar um comutador de Camada 2, comutador de Camada 3 ou um hub, dependendo das suas necessidades e recursos. Se você implantar um comutador, ele deverá ser capaz de encaminhar DHCP ou você deverá colocar um servidor DHCP em cada sub-rede. Se você implantar um hub, estará implantando uma única sub-rede e não precisará do encaminhamento DHCP ou de um segundo escopo no servidor DHCP.

##### <a name="static-tcpip-configurations"></a>Configurações TCP/IP estáticas
Os servidores nesta implantação são configurados com endereços IPv4 estáticos. Os computadores cliente são configurados por padrão para receber concessões de endereço IP do servidor DHCP.

##### <a name="active-directory-domain-services-global-catalog-and-dns-server-dc1"></a>Catálogo global dos Serviços de Domínio Active Directory e servidor DNS DC1
O AD DS (Serviços de Domínio Active Directory) e o DNS (Sistema de Nomes de Domínio) são instalados neste servidor, denominado DC1, que fornece os serviços de diretório e de resolução de nomes para todos os computadores e dispositivos na rede.

##### <a name="dhcp-server-dhcp1"></a>Servidor DHCP DHCP1
O servidor DHCP, denominado DHCP1, está configurado com um escopo que fornece concessões de endereços IP para computadores na sub-rede local. O servidor DHCP pode também ser configurado com escopos adicionais para fornecer concessões de endereços IP para computadores em outras sub-redes quando o encaminhamento DHCP é configurado nos roteadores.

##### <a name="client-computers"></a>Computadores cliente
Os computadores que executam sistemas operacionais cliente do Windows são configurados por padrão como clientes DHCP, que obtêm endereços IP e opções DHCP automaticamente do servidor DHCP.

## <a name="core-network-planning"></a><a name="BKMK_planning"></a>Planejamento da rede principal
Antes de implantar uma rede principal, você deve planejar os itens a seguir.

- [Planejando sub-redes](#bkmk_NetFndtn_Pln_Subnt)

- [Planejando a configuração básica de todos os servidores](#bkmk_NetFndtn_Pln_AllSrvrs)

- [Planejando a implantação do DC1](#bkmk_NetFndtn_Pln_AD-DNS-01)

- [Planejando o acesso de domínio](#bkmk_NetFndtn_Pln_DomAccess)

- [Planejando a implantação do DHCP1](#bkmk_NetFndtn_Pln_DHCP-01)

As seções a seguir fornecem mais detalhes sobre cada um desses itens.

> [!NOTE]
> Para obter assistência com o planejamento de sua implantação, consulte o [Apêndice planilha de preparação de planejamento de rede E-Core](#BKMK_E).

### <a name="planning-subnets"></a><a name="bkmk_NetFndtn_Pln_Subnt"></a>Planejando sub-redes
No sistema de redes dos protocolos TCP/IP, os roteadores são usados para interconectar o hardware e o software usados em segmentos de rede física diferentes chamados sub-redes. Os roteadores também são usados para encaminhar pacotes IP entre cada uma das sub-redes. Determine o layout físico da rede, incluindo o número de roteadores e sub-redes que você precisa, antes de continuar com as instruções deste guia.

Além disso, para configurar os servidores na rede com endereços IP estáticos, determine o intervalo de endereços IP que deseja usar para a sub-rede onde se encontram os servidores da rede principal. Neste guia, os intervalos de endereços IP privados 10.0.0.1-10.0.0.254 e 10.0.1.1-10.0.1.254 são usados como exemplos, mas você pode usar qualquer intervalo de endereços IP privado que preferir.

> [!IMPORTANT]
> Depois de selecionar os intervalos de endereços IP que deseja usar para cada sub-rede, verifique se você pode configurar seus roteadores com o mesmo intervalo de endereços IP usado na sub-rede onde o roteador está instalado. Por exemplo, se seu roteador estiver configurado por padrão com um endereço IP 192.168.1.1, mas você estiver instalando o roteador em uma sub-rede com um intervalo de endereços IP de 10.0.0.0/24, deverá reconfigurar o roteador para usar um endereço IP do intervalo de endereços IP 10.0.0.0/24.

Os seguintes intervalos de endereços IP privados reconhecidos são especificados pela RFC (Request for Comments) da Internet 1918:

- 10.0.0.0-10.255.255.255

- 172.16.0.0-172.31.255.255

- 192.168.0.0-192.168.255.255

Quando você usa os intervalos de endereços IP privados como especificado na RFC 1918, não pode se conectar diretamente à Internet usando um endereço IP privado porque as solicitações desses endereços e para eles são descartadas automaticamente pelos roteadores do ISP (provedor de serviço da Internet). Para adicionar conectividade de Internet à rede principal mais tarde, contrate um ISP para obter um endereço IP público.

> [!IMPORTANT]
> Ao usar endereços IP particulares, você deve usar algum tipo de servidor proxy ou NAT (conversão de endereços de rede) para converter os intervalos de endereços IP privados na rede local para um endereço IP público que pode ser roteado na Internet. A maioria dos roteadores fornecem os serviços NAT; portanto, selecionar um roteador compatível com NAT deve ser bastante simples.

Para obter mais informações, consulte [Planejando a implantação do DHCP1](#bkmk_NetFndtn_Pln_DHCP-01).

### <a name="planning-basic-configuration-of-all-servers"></a><a name="bkmk_NetFndtn_Pln_AllSrvrs"></a>Planejando a configuração básica de todos os servidores
Para cada servidor da rede principal, renomeie o computador e atribua e configure um endereço IPv4 estático e outras propriedades de TCP/IP para o computador.

#### <a name="planning-naming-conventions-for-computers-and-devices"></a>Planejando convenções de nomenclatura para computadores e dispositivos
Para manter a consistência em toda a rede, é uma boa ideia usar nomes consistentes para servidores, impressoras e outros dispositivos. Os nomes de computador podem ser usados para ajudar os usuários e administradores a identificar facilmente a finalidade e a localização do servidor, impressora ou outro dispositivo. Por exemplo, se você tiver três servidores DNS, um em São Francisco, um em Los Angeles e outro em Chicago, você poderá usar o número de local da *função de servidor* Convenção de nomenclatura - *location* - *number*:

- DNS-DEN-01. Este nome representa o servidor DNS em Denver, Colorado. Se os servidores DNS adicionais forem adicionados em Denver, o valor numérico no nome poderá ser incrementado, como no DNS-DEN-02 e no DNS-DEN-03.

- DNS-SPAS-01. Este nome representa o servidor DNS em South Pasadena, Califórnia.

- DNS-ORL-01. Este nome representa o servidor DNS em Orlando, Flórida.

Para este guia, a convenção de nomenclatura do servidor é muito simples e consiste na função de servidor primário e em um número. Por exemplo, o controlador de domínio é denominado DC1 e o servidor DHCP é denominado DHCP1.

Recomendamos que você escolha uma convenção de nomenclatura antes de instalar a rede de núcleo usando este guia.

#### <a name="planning-static-ip-addresses"></a>Planejando endereços IP estáticos
Antes de configurar cada computador com um endereço IP estático, planeje seus intervalos de endereços IP e sub-redes. Além disso, determine os endereços IP dos servidores DNS. Se você planeja instalar um roteador que fornece acesso a outras redes, como sub-redes adicionais ou a Internet, deve saber o endereço IP do roteador, também chamado de gateway padrão, para a configuração do endereço IP estático.

A tabela a seguir fornece valores de exemplo para a configuração de endereço IP estático.

|Itens de configuração|Valores de exemplo|
|-----------------------|------------------|
|Endereço IP|10.0.0.2|
|Máscara de sub-rede|255.255.255.0|
|Gateway padrão (endereço IP do roteador)|10.0.0.1|
|Servidor DNS preferencial|10.0.0.2|

> [!NOTE]
> Se você planeja implantar mais de um servidor DNS, também pode planejar o endereço IP do Servidor DNS Alternativo.

### <a name="planning-the-deployment-of-dc1"></a><a name="bkmk_NetFndtn_Pln_AD-DNS-01"></a>Planejando a implantação do DC1
Estas são as principais etapas de planejamento antes de instalar o AD DS (Serviços de Domínio Active Directory e o DNS no DC1.

#### <a name="planning-the-name-of-the-forest-root-domain"></a>Planejando o nome do domínio raiz da floresta
Uma primeira etapa no processo de design do AD DS é determinar quantas florestas sua organização requer. Uma floresta é o contêiner de nível superior AD DS e consiste em um ou mais domínios que compartilham um esquema comum e um catálogo global. Uma organização pode ter várias florestas, mas para a maioria das organizações, um design de floresta única é o modelo preferido e o mais simples de administrar.

Quando você cria o primeiro controlador de domínio em sua organização, está criando o primeiro domínio (também chamado de domínio raiz da floresta) e a primeira floresta. No entanto, antes de executar esta ação usando este guia, determine o melhor nome de domínio para sua organização. Na maioria dos casos, o nome da organização é usado como o nome de domínio, e, em muitos casos, este nome de domínio está registrado. Se você planeja implantar os servidores Web baseados na Internet externos para fornecer informações e serviços para seus clientes ou parceiros, escolha um nome de domínio que não esteja em uso e registre o nome de domínio, para que sua organização o possua.

#### <a name="planning-the-forest-functional-level"></a>Planejando o nível funcional da floresta
Durante a instalação do AD DS, escolha o nível funcional da floresta que deseja usar. A funcionalidade de domínio e de floresta, inserida no Active Directory do Windows Server 2003, fornece uma maneira de habilitar os recursos de domínio ou de floresta do Active Directory no ambiente de rede. Os diferentes níveis de funcionalidade de domínio e de floresta disponíveis, dependendo do ambiente.

A funcionalidade de floresta habilita os recursos em todos os domínios da floresta. Os seguintes níveis funcionais de floresta estão disponíveis:

-  Windows Server 2008. Esse nível funcional de floresta dá suporte apenas a controladores de domínio que executam o Windows Server 2008 e versões posteriores do sistema operacional Windows Server.

-  Windows Server 2008 R2. Esse nível funcional de floresta dá suporte a controladores de domínio do Windows Server 2008 R2 e controladores de domínio que executam versões posteriores do sistema operacional Windows Server.

-  Windows Server 2012. Esse nível funcional de floresta dá suporte a controladores de domínio do Windows Server 2012 e controladores de domínio que executam versões posteriores do sistema operacional Windows Server.

-  Windows Server 2012 R2. Esse nível funcional de floresta dá suporte a controladores de domínio do Windows Server 2012 R2 e controladores de domínio que executam versões posteriores do sistema operacional Windows Server.

-  Windows Server 2016. Esse nível funcional de floresta dá suporte apenas a controladores de domínio e controladores de domínio do Windows Server 2016 que estão executando versões posteriores do sistema operacional Windows Server.

Se você estiver implantando um novo domínio em uma nova floresta e todos os controladores de domínio estiverem executando o Windows Server 2016, é recomendável configurar AD DS com o nível funcional de floresta do Windows Server 2016 durante a instalação do AD DS.

> [!IMPORTANT]
> Depois que o nível funcional de floresta é aumentado, os controladores de domínio que estão executando os sistemas operacionais anteriores não podem ser introduzidos na floresta. Por exemplo, se você aumentar o nível funcional da floresta para o Windows Server 2016, os controladores de domínio que executam o Windows Server 2012 R2 ou o Windows Server 2008 não poderão ser adicionados à floresta.

Os itens de configuração de exemplo para o AD DS são fornecidos na tabela a seguir.

|Itens de configuração:|Valores de exemplo:|
|------------------------|-------------------|
|Nome DNS completo|Exemplos:<p>-corp.contoso.com<br />-example.com|
|Nível funcional da floresta|-Windows Server 2008 <br />-Windows Server 2008 R2 <br />-Windows Server 2012 <br />-Windows Server 2012 R2 <br />-Windows Server 2016|
|Local da pasta do Banco de Dados dos Serviços de Domínio Active Directory|E:\Configuration\\<p>Ou aceite o local padrão.|
|Local da pasta dos arquivos de Log dos Serviços de Domínio Active Directory|E:\Configuration\\<p>Ou aceite o local padrão.|
|Local da pasta do SYSVOL dos Serviços de Domínio Active Directory|E:\Configuration\\<p>Ou aceite o local padrão.|
|Senha do Administrador do Modo de Restauração de Diretório|**J \* p2leO4 $ F**|
|Nome de arquivo de resposta (opcional)|**AD DS_AnswerFile**|

#### <a name="planning-dns-zones"></a>Planejando zonas DNS
Em servidores DNS primários, integrados ao Active Directory, uma zona de pesquisa direta é criada por padrão durante a instalação da função de Servidor DNS. Uma zona de pesquisa direta permite que computadores e dispositivos consultem o endereço IP de outro computador ou dispositivo com base no seu nome DNS. Além de uma zona de pesquisa direta, recomendamos que você crie uma zona de pesquisa inversa de DNS. Com uma zona de pesquisa inversa de DNS, um computador ou dispositivo pode descobrir o nome de outro computador ou dispositivo usando seu endereço IP. A implantação de uma zona de pesquisa inversa normalmente melhora o desempenho do DNS e aumenta o êxito nas consultas DNS.

Quando você cria uma zona de pesquisa inversa, o domínio in-addr.arpa, que é definido nos padrões DNS e reservado no namespace DNS da Internet para oferecer uma forma prática e confiável de realizar consultas inversas, é configurado no DNS. Para criar o namespace inverso, subdomínios dentro do domínio in-addr.arpa são formados, usando a ordem inversa dos números na notação decimal com ponto de endereços IP.

O domínio in-addr.arpa se aplica a todas as redes TCP/IP baseadas no endereçamento de protocolo Internet versão 4 (IPv4). O Assistente de Nova Zona automaticamente assumirá que você está usando este domínio ao criar uma nova zona de pesquisa inversa.

Enquanto você estiver executando o Assistente de Nova Zona, recomendamos as seguintes seleções:

|Itens de configuração|Valores de exemplo|
|-----------------------|------------------|
|Tipo de zona|**Zona primária** e **Armazenar a zona no Active Directory** estão selecionados|
|Escopo de Replicação de Zona do Active Directory|**Para todos os servidores DNS neste domínio**|
|Página do assistente de Nome da Primeira Zona de Pesquisa Inversa|**Zona de pesquisa inversa do IPv4**|
|Página do assistente de Nome da Segunda Zona de Pesquisa Inversa|ID da Rede = 10.0.0.|
|Atualizações Dinâmicas|**Permitir apenas atualizações dinâmicas seguras**|

### <a name="planning-domain-access"></a><a name="bkmk_NetFndtn_Pln_DomAccess"></a>Planejando o acesso de domínio
Para fazer logon no domínio, o computador deve ser um computador membro do domínio e a conta de usuário deve ser criada no AD DS antes da tentativa de logon.

> [!NOTE]
> Computadores individuais que estão executando o Windows tem um banco de dados local de contas de usuários de grupos e usuários denominado o banco de dados de contas de usuário do SAM (Gerente de Contas de Segurança). Quando você criar uma conta de usuário no computador local no banco de dados do SAM, pode fazer logon no computador local, mas não pode fazer logon em um domínio. As contas de usuário de domínio são criadas com o MMC (Console de Gerenciamento Microsoft) dos Usuários e Computadores do Active Directory em um controlador de domínio, não com os usuários e grupos locais no computador local.

Depois do primeiro logon bem-sucedido com as credenciais de logon do domínio, as configurações de logon persistem, a menos que o computador seja removido do domínio ou as configurações de logon sejam alteradas manualmente.

Antes de você fazer logon no domínio:

- Crie contas de usuários em Usuários e Computadores do Active Directory. Cada usuário deve ter uma conta de usuário dos Serviços de Domínio Active Directory em Usuários e Computadores do Active Directory. Para obter mais informações, consulte [Criar uma conta de usuário em Usuários e Computadores do Active Directory](#BKMK_createUA).

- Verifique a configuração do endereço IP está correta. Para ingressar um computador no domínio, o computador deve ter um endereço IP. Neste guia, os servidores são configurados com endereços IP estáticos e os computadores cliente recebem concessões de endereços IP do servidor DHCP. Por esse motivo, o servidor DHCP deve ser implantado antes que você adicione clientes ao domínio. Para obter mais informações, consulte [Implantando o DHCP1](#BKMK_deployDHCP01).

- Ingresse o computador no domínio. Qualquer computador que fornece ou acessa recursos de rede deve ser ingressado no domínio. Para obter mais informações, consulte [Ingressando computadores servidores no domínio e fazendo logon](#BKMK_joinlogserver) e [Ingressando computadores cliente no domínio e fazendo logon](#BKMK_joinlogclients).

### <a name="planning-the-deployment-of-dhcp1"></a><a name="bkmk_NetFndtn_Pln_DHCP-01"></a>Planejando a implantação do DHCP1
Estas são as principais etapas de planejamento antes de instalar a função de servidor DHCP no DHCP1.

#### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>Planejando os servidores DHCP e o encaminhamento DHCP
Como as mensagens DHCP são mensagens de difusão, elas não são encaminhadas entre as sub-redes por roteadores. Se você tiver várias sub-redes e desejar fornecer o serviço DHCP em cada sub-rede, deverá fazer o seguinte:

- Instalar um servidor DHCP em cada sub-rede

- Configurar roteadores para encaminhar as mensagens de difusão DHCP entre sub-redes e configurar vários escopos no servidor DHCP, um escopo por sub-rede.

Na maioria dos casos, a configuração de roteadores para encaminhar mensagens de difusão DHCP é mais econômica que a implantação de um servidor DHCP em cada segmento físico da rede.

#### <a name="planning-ip-address-ranges"></a>Planejando intervalos de endereços IP
Cada sub-rede deve ter seu próprio intervalo de endereços IP exclusivo. Esses intervalos são representados em um servidor DHCP com escopos.

Um escopo é um agrupamento administrativo de endereços IP para computadores em uma sub-rede que usa o serviço DHCP. O administrador primeiro cria um escopo para cada sub-rede física e, em seguida, usa o escopo para definir os parâmetros usados pelos clientes.

Um escopo tem as seguintes propriedades:

- Um intervalo de endereços IP do qual incluir ou excluir endereços usados para ofertas de concessão de serviço DHCP.

- Uma máscara de sub-rede, que determina o prefixo de sub-rede para um determinado endereço IP.

- Um nome de escopo atribuído quando é criado.

- Valores de duração da concessão, que são atribuídos aos clientes DHCP que recebem endereços IP alocados dinamicamente.

- Qualquer opção de escopo DHCP configurada para atribuição a clientes DHCP, como endereço ID do servidor DNS ou endereço IP do gateway do roteador/padrão.

- As reservas são opcionalmente usadas para garantir que um cliente DHCP sempre receba o mesmo endereço IP.

Antes de implantar os servidores, liste suas sub-redes e o intervalo de endereços IP que você deseja usar para cada sub-rede.

#### <a name="planning-subnet-masks"></a>Planejando máscaras de sub-rede
As IDs de rede e IDs de host são diferenciadas usando uma máscara de sub-rede. Cada máscara de sub-rede é um número de 32 bits que usa grupos de bits consecutivos de todos (1) para identificar a ID da rede e todos os zeros (0) para identificar as partes de ID do host de um endereço IP.

Por exemplo, a máscara de sub-rede normalmente usada com o endereço IP 131.107.16.200 é o seguinte número binário de 32 bits:

```
11111111 11111111 00000000 00000000
```

Esse número de máscara de sub-rede são 16 bits de um seguidos de 16 bits de zero, indicando que as seções de ID da rede e as seções de ID do host desse endereço IP têm 16 bits de comprimento. Normalmente, essa máscara de sub-rede é exibida em notação decimal com ponto como 255.255.0.0.

A tabela a seguir exibe as máscaras de sub-rede para as classes de endereço de Internet.

|Classe de endereço|Bits para máscara de sub-rede|Máscara de sub-rede|
|-----------------|------------------------|---------------|
|Classe A|11111111 00000000 00000000 00000000|255.0.0.0|
|Classe B|11111111 11111111 00000000 00000000|255.255.0.0|
|Classe C|11111111 11111111 11111111 00000000|255.255.255.0|

Quando você cria um escopo no DHCP e insere o intervalo de endereços IP do escopo, o DHCP fornece esses valores de máscara de sub-rede padrão. Normalmente, os valores de máscara de sub-rede padrão são aceitáveis para a maioria das redes sem requisitos especiais e onde cada segmento de rede IP corresponde a uma única rede física.

Em alguns casos, você pode usar máscaras de sub-rede personalizadas para implementar a criação de sub-redes IP. Com a criação de sub-redes IP, você pode subdividir a parte padrão de ID de host de um endereço IP para especificar sub-redes, que são subdivisões de ID de rede baseada na classe original.

Personalizando o comprimento da máscara de sub-rede, você pode reduzir o número de bits que são usados para o ID de host real.

Para evitar a solução e o roteamento de problemas, verifique se todos os computadores TCP/IP em um segmento de rede usam a mesma máscara de sub-rede e se cada computador ou dispositivo tem um endereço IP exclusivo.

#### <a name="planning-exclusion-ranges"></a>Planejando intervalos de exclusão
Quando você cria um escopo em um servidor DHCP, pode especificar um intervalo de endereços IP que inclui todos os endereços IP que o servidor DHCP pode conceder aos clientes DHCP, como computadores e outros dispositivos. Se você acessar e configurar manualmente alguns servidores e outros dispositivos com endereços IP estáticos do mesmo intervalo de endereços IP usado pelo servidor DHCP, poderá criar acidentalmente um conflito de endereços IP, onde você e o servidor DHCP atribuem o mesmo endereço IP a dispositivos diferentes.

Para resolver esse problema, você pode criar um intervalo de exclusão para o escopo DHCP. Um intervalo de exclusão é um intervalo contíguo de endereços IP dentro do intervalo de endereços IP do escopo que o servidor DHCP não tem permissão para usar. Se você criar um intervalo de exclusão, o servidor DHCP não atribuirá os endereços nesse intervalo, permitindo que você atribua manualmente esses endereços sem criar um conflito de endereços IP.

Você pode excluir endereços IP da distribuição pelo servidor DHCP, criando um intervalo de exclusão para cada escopo. Use as exclusões para todos os dispositivos configurados com um endereço IP estático. Os endereços excluídos devem incluir todos os endereços IP que você atribuiu manualmente a outros servidores, clientes não-DHCP, estações de trabalho sem disco ou clientes de Roteamento, Acesso Remoto e PPP.

Recomendamos que você configure o intervalo de exclusão com endereços extras para acomodar o crescimento futuro da rede. A tabela a seguir fornece um intervalo de exclusão de exemplo para um escopo com um intervalo de endereços IP 10.0.0.1 a 10.0.0.254 e uma máscara de sub-rede de 255.255.255.0.

|Itens de configuração|Valores de exemplo|
|-----------------------|------------------|
|Endereço IP Inicial do intervalo de exclusão|10.0.0.1|
|Endereço IP Final do intervalo de exclusão|endereços 10.0.0.25|

#### <a name="planning-tcpip-static-configuration"></a>Planejando a configuração estática do TCP/IP
Certos dispositivos, como roteadores, servidores DHCP e servidores DNS, devem ser configurados com um endereço IP estático. Além disso, você pode ter dispositivos adicionais, como impressoras, onde deve garantir sempre o mesmo endereço IP. Liste os dispositivos que você deseja configurar estaticamente para cada sub-rede e planeje o intervalo de exclusão que deseja usar no servidor DHCP para garantir que o servidor DHCP não conceda o endereço IP de um dispositivo configurado estaticamente. Um intervalo de exclusão é uma sequência limitada de endereços IP dentro de um escopo, excluído das ofertas de serviço DHCP. Os intervalos de exclusão garantem que os endereços nesses intervalos não sejam oferecidos pelo servidor a clientes DHCP na sua rede.

Por exemplo, se o intervalo de endereços IP de uma sub-rede for 192.168.0.1 a 192.168.0.254 e você tiver dez dispositivos que deseja configurar com um endereço IP estático, poderá criar um intervalo de exclusão para o escopo 192.168.0.*x* que inclui dez ou mais endereços IP: 192.168.0.1 a 192.168.0.15.

Neste exemplo, você usa dez dos endereços IP excluídos para configurar servidores e outros dispositivos com endereços IP estáticos e cinco endereços IP adicionais ficam disponíveis para uma configuração estática de novos dispositivos que você possa desejar adicionar no futuro. Com este intervalo de exclusão, o servidor DHCP fica com um pool de endereços de 192.168.0.16 até 192.168.0.254.

Itens de configuração de exemplo adicionais para o AD DS e o DNS são fornecidos na tabela a seguir.

|Itens de configuração|Valores de exemplo|
|-----------------------|------------------|
|Ligações de Conexão de Rede|Ethernet|
|Configurações do servidor DNS|DC1.corp.contoso.com|
|Endereço IP do servidor DNS preferencial|10.0.0.2|
|Adicionar valores da caixa de diálogo Escopo<p>1. nome do escopo<br />2. endereço IP inicial<br />3. endereço IP final<br />4. máscara de sub-rede<br />5. gateway padrão (opcional)<br />6. duração da concessão|1. sub-rede primária<br />2.10.0.0.1<br />3.10.0.0.254<br />4.255.255.255.0<br />5.10.0.0.1<br />6.8 dias|
|Modo de Operação do Servidor DHCP IPv6|não ativado|

## <a name="core-network-deployment"></a><a name="BKMK_deployment"></a>Implantação da rede principal
Para implantar uma rede principal, estas são as etapas básicas:

1.  [Configurando todos os servidores](#BKMK_configuringAll)

2.  [Implantando o DC1](#BKMK_deployADDNS01)

3.  [Ingressando computadores servidores no domínio e fazendo logon](#BKMK_joinlogserver)

4.  [Implantando o DHCP1](#BKMK_deployDHCP01)

5.  [Ingressando computadores clientes no domínio e fazendo logon](#BKMK_joinlogclients)

6.  [Implantando recursos opcionais para a autenticação do acesso à rede e dos serviços Web](#BKMK_optionalfeatures)

> [!NOTE]
> - Comandos equivalentes do Windows PowerShell são fornecidos para a maioria dos procedimentos neste guia. Antes de executar esses cmdlets no Windows PowerShell, substitua os valores de exemplo pelos valores que são apropriados para sua implantação de rede. Além disso, insira cada cmdlet em uma única linha no Windows PowerShell. Neste guia, cmdlets individuais podem aparecer em várias linhas devido à formatação de restrições e à exibição do documento por outro aplicativo ou navegador.
> - Os procedimentos deste guia não incluem instruções para os casos em que a caixa de diálogo **Controle de Conta de Usuário** é aberta para solicitar sua permissão para continuar. Caso essa caixa de diálogo seja aberta durante a execução dos procedimentos deste guia e em resposta às suas ações, clique em **Continuar**.

### <a name="configuring-all-servers"></a><a name="BKMK_configuringAll"></a>Configurando todos os servidores
Antes de instalar outras tecnologias, como os Serviços de Domínio Active Directory ou o DHCP, é importante configurar os itens a seguir.

- [Renomear o computador](#BKMK_rename)

- [Configurar um endereço IP estático](#BKMK_ip)

Você pode usar as seções a seguir para executar essas ações em cada servidor.

A associação a **Administradores** ou equivalente é o requisito mínimo para a execução destes procedimentos.

#### <a name="rename-the-computer"></a><a name="BKMK_rename"></a>Renomear o computador
Você pode usar o procedimento nesta seção para alterar o nome de um computador. Renomear o computador é útil quando o sistema operacional cria automaticamente um nome de computador que você deseja usar.

> [!NOTE]
> Para executar este procedimento usando o Windows PowerShell, abra o PowerShell, digite os cmdlets a seguir em linhas separadas e pressione ENTER. Você também deve substituir *Nome_do_Computador* pelo nome que deseja usar.
>
> `Rename-Computer`*ComputerName*
>
> `Restart-Computer`

###### <a name="to-rename-computers-running-windows-server-2016-windows-server-2012-r2-and-windows-server-2012"></a>Para renomear computadores que executam o Windows Server 2016, o Windows Server 2012 R2 e o Windows Server 2012

1.  No Gerenciador do Servidor, clique em **Servidor Local**. As **Propriedades** do computador são exibidas no painel de detalhes.

2.  Em **Propriedades**, em **Nome do computador**, clique no nome existente. A caixa de diálogo **Propriedades do Sistema** será aberta. Clique em **Alterar**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** será aberta.

3.  Na caixa de diálogo **Alterações de Nome/Domínio do Computador**, no **Nome do computador**, digite um novo nome para o computador. Por exemplo, se você deseja denominar o computador como DC1, digite **DC1**.

4.  Clique em **OK** duas vezes e depois em **Fechar**. Se você deseja reiniciar o computador imediatamente para concluir a alteração de nome, clique em **Reiniciar Agora**. Caso contrário, clique em **Reiniciar Mais Tarde**.

> [!NOTE]
> Para obter informações sobre como renomear computadores que executam outros sistemas operacionais da Microsoft, consulte [o apêndice a-](#BKMK_A)renomeando computadores.

#### <a name="configure-a-static-ip-address"></a><a name="BKMK_ip"></a>Configurar um endereço IP estático
Você pode usar os procedimentos neste tópico para configurar as propriedades do protocolo IP versão 4 (IPv4) de uma conexão de rede com um endereço estático para computadores que executam o Windows Server 2016.

> [!NOTE]
> Para executar este procedimento usando o Windows PowerShell, abra o PowerShell, digite os cmdlets a seguir em linhas separadas e pressione ENTER. Você também deve substituir os nomes de interface e os endereços IP neste exemplo pelos valores que deseja usar para configurar o seu computador.
>
> `New-NetIPAddress -IPAddress 10.0.0.2 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`
>
> `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 127.0.0.1`

###### <a name="to-configure-a-static-ip-address-on-computers-running-windows-server-2016-windows-server-2012-r2-and-windows-server-2012"></a>Para configurar um endereço IP estático em computadores que executam o Windows Server 2016, o Windows Server 2012 R2 e o Windows Server 2012

1.  Na barra de tarefas, clique com o botão direito do mouse no ícone Rede e clique em **Abrir a Central de Rede e Compartilhamento**.

2.  Em  **central de rede e compartilhamento**, clique em **alterar configurações do adaptador**. A pasta **Conexões de Rede** é aberta e exibe as conexões de rede disponíveis.

3.  Em **Conexões de Rede**, clique com o botão direito do mouse na conexão que deseja configurar e clique em **Propriedades**. A caixa de diálogo **Propriedades** da conexão de rede é aberta.

4.  Na caixa de diálogo **Propriedades** da conexão de rede, em **Esta conexão utiliza os seguintes itens**, selecione **Protocolo TCP/IPv4 (TCP/IP Versão 4)** e clique em **Propriedades**. A caixa de diálogo **Propriedades do Protocolo TCP/IPv4 (TCP/IP Versão 4)** será aberta.

5.  Em **Propriedades do Protocolo TCP/IPv4 (TCP/IP Versão 4)**, na guia **Geral**, clique em **Usar o seguinte endereço IP**. Em **Endereço IP**, digite o endereço IP que deseja usar.

6.  Pressione Tab para colocar o cursor em **Máscara de sub-rede**. Um valor padrão para máscara de sub-rede será inserido automaticamente. Aceite a máscara de sub-rede padrão ou digite a máscara de sub-rede que deseja usar.

7.  No **Gateway padrão**, digite o endereço IP do seu gateway padrão.

    > [!NOTE]
    > Configure o **Gateway padrão** com o mesmo endereço IP usado na interface de LAN (rede de área local) do seu roteador. Por exemplo, se você tiver um roteador que está conectado a uma WAN (rede de longa distância), como a Internet, bem como a sua LAN, configure a interface de LAN com o mesmo endereço IP que você especificará como o **Gateway padrão**. Em outro exemplo, se você tiver um roteador que está conectado a duas LANs, onde a LAN A usa o intervalo de endereços 10.0.0.0/24 e a LAN B usa o intervalo de endereços 192.168.0.0/24, configure a LAN A com um endereço de IP de roteador a partir desse intervalo de endereço, como 10.0.0.1. Além disso, no escopo DHCP desse intervalo de endereços, configure o **Gateway padrão** com o endereço IP 10.0.0.1. Para a LAN B, configure a interface do roteador da LAN B com um endereço desse intervalo de endereços, como 192.168.0.1, e configure o escopo da LAN B 192.168.0.0/24 com um valor de **Gateway padrão** de 192.168.0.1.

8.  Em **Servidor DNS preferencial**, digite o endereço IP do seu servidor DNS. Se você planeja usar o computador local como o servidor DNS preferencial, digite o endereço IP do computador local.

9. Em **Servidor DNS alternativo**, digite o endereço IP do seu servidor DNS alternativo, se houver. Se você planeja usar o computador local como um servidor DNS alternativo, digite o endereço IP do computador local.

10. Clique em **OK** e então clique em **Fechar**.

> [!NOTE]
> Para obter informações sobre como configurar um endereço IP estático em computadores que executam outros sistemas operacionais da Microsoft, consulte o [Apêndice B-Configurando endereços IP estáticos](#BKMK_B).

#### <a name="deploying-dc1"></a><a name="BKMK_deployADDNS01"></a>Implantando o DC1
Para implantar o DC1, que é o computador que executa o AD DS (Serviços de Domínio Active Directory) e o DNS, conclua estas etapas na seguinte ordem:

- Siga as etapas na seção [Configurando todos os servidores](#BKMK_configuringAll).

- [Instalar o AD DS e o DNS para uma Nova Floresta](#BKMK_installAD-DNS)

- [Criar uma Conta de Usuário em Usuários e Computadores do Active Directory](#BKMK_createUA)

- [Atribuir a associação ao grupo](#BKMK_assigngroup)

- [Configurar uma zona de pesquisa inversa de DNS](#BKMK_reverse)

**Privilégios administrativos**

Se você estiver instalando uma rede pequena e for o único administrador da rede, recomendamos que crie uma conta de usuário para si mesmo e adicione sua conta de usuário como um membro dos Administradores de Empresa e Administradores do Domínio. Isso tornará mais fácil para você atuar como o administrador de todos os recursos de rede. Também recomendamos que você faça logon com essa conta somente quando precisar executar tarefas administrativas e crie uma conta de usuário separada para executar outras tarefas relacionadas.

Se você tem uma organização maior com vários administradores, consulte a documentação do AD DS para determinar a melhor associação de grupo para os funcionários da organização.

**Diferenças entre contas de usuário de domínio e contas de usuário no computador local**

Uma das vantagens de uma infraestrutura baseada em domínio é que você não precisa criar contas de usuário em cada computador no domínio. Isso é verdadeiro quando o computador é um computador cliente ou um servidor.

Devido a isso, você não deve criar contas de usuário em cada computador no domínio. Crie todas as contas de usuário em Usuários e Computadores do Active Directory e use os procedimentos anteriores para atribuir a associação de grupo. Por padrão, todas as contas de usuário são membros do grupo Usuários do Domínio.

Todos os membros do grupo Usuários do Domínio podem fazer logon em qualquer computador cliente depois que ele é associado ao domínio.

Você pode configurar contas de usuário para designar os dias e horários em que o usuário tem permissão para fazer logon no computador. Você também pode designar que computadores cada usuário tem permissão para usar. Para definir essas configurações, abra Usuários e Computadores do Active Directory, localize a conta de usuário que deseja configurar e clique duas vezes na conta. Em **Propriedades** da conta de usuário, clique na guia **Conta** e clique em **Horário de Logon** ou em **Fazer Logon em**.

#### <a name="install-ad-ds-and-dns-for-a-new-forest"></a><a name="BKMK_installAD-DNS"></a>Instalar o AD DS e o DNS para uma Nova Floresta

Você pode usar um dos procedimentos a seguir para instalar Active Directory Domain Services (AD DS) e DNS e para criar um novo domínio em uma nova floresta.

O primeiro procedimento fornece instruções sobre como executar essas ações usando o Windows PowerShell, enquanto o segundo procedimento mostra como instalar AD DS e DNS usando Gerenciador do Servidor.

>[!IMPORTANT]
>Depois de concluir a execução das etapas neste procedimento, o computador será reiniciado automaticamente.

**Instalar AD DS e DNS usando o Windows PowerShell**

Você pode usar os comandos a seguir para instalar e configurar o AD DS e o DNS. Você deve substituir o nome de domínio neste exemplo pelo valor que deseja usar para o seu domínio.

>[!NOTE]
>Para obter mais informações sobre esses comandos do Windows PowerShell, consulte os tópicos de referência a seguir.
>- [Install-WindowsFeature](/powershell/module/servermanager/install-windowsfeature)
>- [Install-ADDSForest](/powershell/module/addsdeployment/install-addsforest)

O mínimo necessário para executar este procedimento é ser membro do grupo **Administradores**.

- Execute o Windows PowerShell como administrador, digite o seguinte comando e pressione ENTER:

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools`
```

Quando a instalação for concluída com êxito, a seguinte mensagem será exibida no Windows PowerShell.

| Êxito | Reinicialização necessária | Código de Saída |  Resultado do recurso |
|--|--|--|--|
| True | Não | Êxito | {Active Directory Domain Services, grupo P... |

- No Windows PowerShell, digite o comando a seguir, substituindo o texto **Corp.contoso.com** pelo seu nome de domínio e, em seguida, pressione ENTER:

````powershell
Install-ADDSForest -DomainName "corp.contoso.com"
````

- Durante o processo de instalação e configuração, que é visível na parte superior da janela do Windows PowerShell, o prompt a seguir é exibido. Depois de aparecer, digite uma senha e pressione ENTER.

    **SafeModeAdministratorPassword:**

- Depois de digitar uma senha e pressionar ENTER, o prompt de confirmação a seguir será exibido. Digite a mesma senha e pressione ENTER.

    **Confirmar SafeModeAdministratorPassword:**

- Quando o prompt a seguir for exibido, digite a letra **Y** e pressione Enter.

    ```
    The target server will be configured as a domain controller and restarted when this operation is complete.
    Do you want to continue with this operation?
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    ```

- Se desejar, você pode ler as mensagens de aviso que são exibidas durante a instalação normal e bem-sucedida de AD DS e DNS. Essas mensagens são normais e não são uma indicação de falha de instalação.

- Depois que a instalação for realizada com sucesso, será exibida uma mensagem informando que você está prestes a ser desconectado do computador para que o computador possa ser reiniciado. Se você clicar em **fechar**, você estará imediatamente conectado ao computador e o computador será reiniciado. Se você não clicar em **fechar**, o computador será reiniciado após um período de tempo padrão.

- Depois que o servidor for reiniciado, você poderá verificar a instalação bem-sucedida do Active Directory Domain Services e do DNS. Abra o Windows PowerShell, digite o comando a seguir e pressione ENTER.

````powershell
Get-WindowsFeature
````

Os resultados desse comando são exibidos no Windows PowerShell e devem ser semelhantes aos resultados na imagem abaixo. Para tecnologias instaladas, os colchetes à esquerda do nome da tecnologia contêm o caractere **X** e o valor do **estado de instalação** é **instalado**.

![Resultados do comando Get-WindowsFeature](../media/Core-Network-Guide/server-roles-installed.jpg)

**Instalar AD DS e DNS usando Gerenciador do Servidor**

1.  No DC1, no **Gerenciador do Servidor**, clique em **Gerenciar** e em **Adicionar Funções e Recursos**. O Assistente para Adicionar Funções e Recursos é aberto.

2.  Em **Antes de Começar**, clique em **Avançar**.

    > [!NOTE]
    > A página **Antes de Começar** do Assistente para Adicionar Funções e Recursos não é exibida quando você marca a opção **Ignorar esta página por padrão** quando o Assistente para Funções e Recursos foi executado.

3.  Em **Selecionar Tipo de Instalação**, verifique se **Instalação baseada em função ou recurso** está marcada e clique em **Avançar**.

4.  Em **Selecionar servidor de destino**, verifique se **Selecionar um servidor no pool de servidores** está marcada. Em **Pool de Servidores**, verifique se o computador local está selecionado. Clique em **Avançar**.

5.  Em **Selecionar funções de servidor**, em **Funções**, clique em **Serviços de Domínio Active Directory**. Em **Adicionar recursos que são necessários para Serviços de Domínio Active Directory**, clique em **Adicionar Recursos**. Clique em **Avançar**.

6.  Em **Selecionar recursos**, clique em **Avançar** e, em **Serviços de Domínio Active Directory**, analise as informações fornecidas e clique em **Avançar**.

7.  Em **Confirmar seleções de instalação**, clique em **Instalar**. A página Progresso da instalação exibe o status durante o processo de instalação. Quando o processo é concluído, nos detalhes da mensagem, clique em **Promover este servidor a um controlador de domínio**. O Assistente de Configuração dos Serviços de Domínio Active Directory é aberto.

8.  Em **Configuração de Implantação**, selecione **Adicionar uma nova floresta**. Em **Nome do domínio raiz**, digite o FQDN (nome de domínio totalmente qualificado do seu domínio. Por exemplo, se o FQDN for corp.contoso.com, digite **corp.contoso.com**. Clique em **Avançar**.

9. Em **Opções do Controlador de Domínio**, em **Selecionar nível funcional da nova floresta e do domínio raiz**, selecione o nível funcional da floresta e o nível funcional do domínio que você deseja usar. Em **Especificar recursos do controlador de domínio**, verifique se as opções **Servidor do Sistema de Nomes de Domínio (DNS)** e **Catálogo Global (GC)** estão marcadas. Em **Senha** e **Confirmar senha**, digite a senha do DSRM (Modo de Restauração de Serviços de Diretório) que você deseja usar. Clique em **Avançar**.

10. Em **Opções do DNS**, clique em **Avançar**.

11. Em **Opções Adicionais**, verifique o nome NetBIOS atribuído ao domínio e o altere quando necessário. Clique em **Avançar**.

12. Em **Caminhos**, em **Especificar o local do banco de dados do AD DS, arquivos de log e SYSVOL**, execute um destes procedimentos:

    - Aceite os valores padrão.

    - Digite os locais de pasta que deseja usar para a **Pasta do banco de dados**, **Pasta dos arquivos de log** e **Pasta SYSVOL**.

13. Clique em **Avançar**.

14. Em **Examinar Opções**, analise suas seleções.

15. Se você deseja exportar as configurações para um script do Windows PowerShell, clique em **Exibir script**. O script é aberto no Bloco de Notas e você pode salvá-lo no local de pasta desejado. Clique em **Avançar**. Em **Verificação de Pré-Requisitos**, suas seleções são validadas. Quando a verificação for concluída, clique em **Instalar**. Quando o Windows solicitar, clique em **Fechar**. O servidor é reiniciado para concluir a instalação de AD DS e DNS.

16. Para verificar a instalação bem-sucedida, exiba o console do Gerenciador do Servidor após a reinicialização do servidor. O AD DS e o DNS devem aparecer no painel esquerdo, como os itens destacados na imagem abaixo.

![AD DS e DNS em Gerenciador do Servidor](../media/Core-Network-Guide/server-roles-installed-sm.jpg)

##### <a name="create-a-user-account-in-active-directory-users-and-computers"></a><a name="BKMK_createUA"></a>Criar uma Conta de Usuário em Usuários e Computadores do Active Directory
Você pode usar este procedimento para criar uma nova conta de usuário de domínio no MMC (Console de Gerenciamento Microsoft) Usuários e Computadores do Active Directory.

A associação a **Adminis. do Domínio** ou equivalente é o requisito mínimo para a execução deste procedimento.

> [!NOTE]
> Para executar este procedimento usando o Windows PowerShell, abra o PowerShell, digite o cmdlet a seguir em uma linha e pressione ENTER. Você também deve substituir o nome da conta de usuário neste exemplo pelo valor que você deseja usar.
>
> `New-ADUser -SamAccountName User1 -AccountPassword (read-host "Set user password" -assecurestring) -name "User1" -enabled $true -PasswordNeverExpires $true -ChangePasswordAtLogon $false`
>
> Depois de pressionar ENTER, digite a senha da conta de usuário. A conta é criada e, por padrão, é concedida a associação ao grupo Usuários do Domínio.
>
> Com o cmdlet a seguir, você pode atribuir membros de grupos adicionais à nova conta de usuário. O exemplo a seguir adiciona User1 aos grupos Administradores do Domínio e Administradores de Empresa. Antes de executar esse comando, altere o nome de conta de usuário, o nome do domínio e os grupos para atender às suas necessidades.
>
> `Add-ADPrincipalGroupMembership -Identity "CN=User1,CN=Users,DC=corp,DC=contoso,DC=com" -MemberOf "CN=Enterprise Admins,CN=Users,DC=corp,DC=contoso,DC=com","CN=Domain Admins,CN=Users,DC=corp,DC=contoso,DC=com"`

###### <a name="to-create-a-user-account"></a>Para criar uma conta de usuário

1.  No DC1, no Gerenciador do Servidor, clique em **Ferramentas** e em **Usuários e Computadores do Active Directory**. O MMC Usuários e Computadores do Active Directory é aberto. Caso ainda não esteja selecionado, clique no nó do seu domínio. Por exemplo, se o domínio for corp.contoso.com, clique em **corp.contoso.com**.

2.  No painel de detalhes, clique com o botão direito do mouse na pasta em que você deseja adicionar uma conta de usuário.

    **Posição?**

    - Active Directory a pasta usuários e computadores/*nó do domínio* / *folder*

3.  Aponte para **Novo** e clique em **Usuário**. A caixa de diálogo **novo objeto – usuário** é aberta.

4.  Em **Nome**, digite o nome do usuário.

5.  Em **Iniciais**, digite as iniciais do usuário.

6.  Em **Sobrenome**, digite o sobrenome do usuário.

7.  Modifique **Nome completo** para adicionar iniciais ou inverter a ordem do primeiro e do último nome.

8.  Em **Nome de logon do usuário**, digite o nome de logon do usuário. Clique em **Avançar**.

9. Em **Novo Objeto - Usuário**, em **Senha** e em **Confirmar senha**, digite a senha do usuário e selecione as opções de senha apropriadas.

10. Clique em **Avançar**, analise as configurações da nova conta de usuário e clique em **Concluir**.

##### <a name="assign-group-membership"></a><a name="BKMK_assigngroup"></a>Atribuir a associação ao grupo
Você pode usar este procedimento para adicionar um usuário, computador ou grupo a um grupo no MMC (Console de Gerenciamento Microsoft) Usuários e Computadores do Active Directory.

A associação a **Adminis. do Domínio** ou equivalente é o requisito mínimo para a execução deste procedimento.

###### <a name="to-assign-group-membership"></a>Atribuir a associação ao grupo

1.  No DC1, no Gerenciador do Servidor, clique em **Ferramentas** e em **Usuários e Computadores do Active Directory**. O MMC Usuários e Computadores do Active Directory é aberto. Caso ainda não esteja selecionado, clique no nó do seu domínio. Por exemplo, se o domínio for corp.contoso.com, clique em **corp.contoso.com**.

2.  No painel de detalhes, clique duas vezes na pasta que contém o grupo ao qual deseja adicionar um membro.

    Onde?

    - **Active Directory usuários e computadores** / *nó* / de domínio *pasta que contém o grupo*

3.  No painel de detalhes, clique com o botão direito do mouse no objeto que deseja adicionar a um grupo, como um usuário ou computador e clique em **Propriedades**. A caixa de diálogo **Propriedades** do objeto é aberta. Clique na guia **Membro de**.

4.  Na guia **Membro de**, clique em **Adicionar**.

5.  Em **Insira os nomes de objeto a serem selecionados**, digite o nome do grupo ao qual você deseja adicionar o objeto e clique em **OK**.

6.  Para atribuir a associação de grupo a outros usuários, grupos ou computadores, repita as etapas 4 e 5 deste procedimento.

##### <a name="configure-a-dns-reverse-lookup-zone"></a><a name="BKMK_reverse"></a>Configurar uma zona de pesquisa inversa de DNS
Você pode usar este procedimento para configurar uma zona de pesquisa inversa no DNS (Sistema de Nome de Domínio).

O mínimo necessário para executar este procedimento é ser membro do grupo **Adminis. do Domínio**.

> [!NOTE]
> - Para organizações de médio e grande porte, é recomendável que você configure e use o grupo DNSAdmins em Active Directory usuários e computadores. Para obter mais informações, consulte [Recursos técnicos adicionais](#BKMK_resources).
> - Para executar este procedimento usando o Windows PowerShell, abra o PowerShell, digite o cmdlet a seguir em uma linha e pressione ENTER. Você também deve substituir os nomes da zona de pesquisa inversa DNS e do arquivo de zona neste exemplo pelos valores que deseja usar. Verifique se você inverteu a ID de rede para o nome de zona inversa. Por exemplo, se a ID de rede for 192.168.0, crie o nome da zona de pesquisa inversa **0.168.192.in-addr. arpa**.
>
> `Add-DnsServerPrimaryZone 0.0.10.in-addr.arpa -ZoneFile 0.0.10.in-addr.arpa.dns`

###### <a name="to-configure-a-dns-reverse-lookup-zone"></a>Para configurar uma zona de pesquisa inversa de DNS

1.  No DC1, no Gerenciador do Servidor, clique em **Ferramentas** e em **DNS**. O MMS DNS é aberto.

2.  No DNS, clique duas vezes no nome do servidor para expandir a árvore, se ela ainda não estiver expandida. Por exemplo, se o nome do Servidor DNS for DC1, clique duas vezes em **DC1**.

3.  Selecione **Zonas de Pesquisa Inversa**, clique com o botão direito do mouse em **Zonas de Pesquisa Inversa** e clique em **Nova Zona**. O Assistente de Nova Zona se abre.

4.  Em **Bem-vindo ao Assistente de Nova Zona**, clique em **Avançar**.

5.  Em **Tipo de Zona**, selecione **Zona primária**.

6.  Se o servidor DNS for um controlador de domínio gravável, verifique se a opção **Armazenar a zona no Active Directory** está marcada. Clique em **Avançar**.

7.  Em **Escopo de Replicação de Zona do Active Directory**, selecione **Para todos os servidores DNS sendo executados em controladores de domínio neste domínio**, a menos que você tenha um motivo específico para escolher uma opção diferente. Clique em **Avançar**.

8.  Na primeira página de **Nome da Zona de Pesquisa Inversa**, selecione **Zona de Pesquisa Inversa IPv4**. Clique em **Avançar**.

9. Na segunda página de **Nome da Zona de Pesquisa Inversa**, selecione uma das seguintes opções:

    - Em **Identificação de rede**, digite a identificação de rede do seu intervalo de endereços IP. Por exemplo, se o intervalo de endereços IP for 10.0.0.1 a 10.0.0.254, digite **10.0.0**.

    - Em **Nome da zona de pesquisa inversa**, seu nome da zona de pesquisa inversa IPv4 é adicionado automaticamente. Clique em **Avançar**.

10. Em **Atualização Dinâmica**, selecione o tipo de atualizações dinâmicas que serão permitidas. Clique em **Avançar**.

11. Em **Concluindo o Assistente de Nova Zona**, verifique suas escolhas e clique em **Concluir**.

#### <a name="joining-server-computers-to-the-domain-and-logging-on"></a><a name="BKMK_joinlogserver"></a>Ingressando computadores servidores no domínio e fazendo logon
Depois de ter instalado o AD DS (Serviços de Domínio Active Directory) e criado uma ou mais contas de usuário que tem permissões para ingressar um computador no domínio, você poderá ingressar servidores de rede principal no domínio e fazer logon em servidores para instalar tecnologias adicionais, como o protocolo DHCP.

Em todos os servidores que você estiver implantando, exceto no servidor que executa o AD DS, faça o seguinte:

1.  Conclua os procedimentos fornecidos em [Configurando todos os servidores](#BKMK_configuringAll).

2.  Use as instruções nos dois seguintes procedimentos para ingressar seus servidores no domínio e fazer logon nos servidores para executar tarefas de implantação adicionais:

> [!NOTE]
> Para executar este procedimento usando o Windows PowerShell, abra o PowerShell, digite o cmdlet a seguir e pressione ENTER. Você também deve substituir o nome do domínio pelo nome que deseja usar.
>
> `Add-Computer -DomainName corp.contoso.com`
>
> Quando você for solicitado a fazê-lo, digite o nome de usuário e a senha de uma conta que tenha permissão para ingressar um computador no domínio. Para reiniciar o computador, digite o comando a seguir e pressione ENTER.
>
> `Restart-Computer`

###### <a name="to-join-computers-running--windows-server-2016--windows-server-2012-r2--and--windows-server-2012--to-the-domain"></a>Para unir computadores que executam o Windows Server 2016, o Windows Server 2012 R2 e o Windows Server 2012 ao domínio

1.  No Gerenciador do Servidor, clique em **Servidor Local**. No painel de detalhes, clique em **Grupo de Trabalho**. A caixa de diálogo **Propriedades do Sistema** será aberta.

2.  Na caixa de diálogo **Propriedades do Sistema**, clique em **Alterar**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** será aberta.

3.  No **Nome do Computador**, em **Membro de**, clique em **Domínio** e digite o nome do domínio no qual você deseja ingressar. Por exemplo, se o nome do domínio for corp.contoso.com, digite **corp.contoso.com**.

4.  Clique em **OK**. A caixa de diálogo **Segurança do Windows** será aberta.

5.  Em **Alterações de Nome/Domínio do Computador**, em **Nome de usuário**, digite o nome de usuário, digite a senha no campo **Senha** e clique em **OK**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** é aberta, dando as boas-vindas ao domínio. Clique em **OK**.

6.  A caixa de diálogo **Alterações de Nome/Domínio do Computador** exibe uma mensagem indicando que você deve reiniciar o computador para aplicar as alterações. Clique em **OK**.

7.  Na caixa de diálogo **Propriedades do Sistema**, na guia **Nome do Computador**, clique em **Fechar**. A caixa de diálogo **Microsoft Windows** é aberta e exibe uma mensagem, indicando novamente que você deve reiniciar o computador para aplicar as alterações. Clique em **Reiniciar Agora**.

> [!NOTE]
> Para obter informações sobre como unir computadores que estão executando outros sistemas operacionais da Microsoft ao domínio, consulte o [Apêndice C-unindo computadores ao domínio](#BKMK_C).

###### <a name="to-log-on-to-the-domain-using-computers-running-windows-server-2016"></a>Para fazer logon no domínio usando computadores que executam o Windows Server 2016

1.  Faça logoff do computador ou o reinicie.

2.  Pressione CTRL + ALT + DELETE. A tela de logon é exibida.

3.  No canto inferior esquerdo, clique em **outro usuário**.

4.  Em **nome de usuário**, digite seu nome de usuário.

5.  Em **Senha**, digite sua senha do domínio e clique na seta ou pressione ENTER.

> [!NOTE]
> Para obter informações sobre como fazer logon no domínio usando computadores que executam outros sistemas operacionais da Microsoft, consulte o [Apêndice D – fazer logon no domínio](#BKMK_D).

#### <a name="deploying-dhcp1"></a><a name="BKMK_deployDHCP01"></a>Implantando o DHCP1
Antes de implantar este componente da rede principal, faça o seguinte:

- Siga as etapas na seção [Configurando todos os servidores](#BKMK_configuringAll).

- Siga as etapas na seção [Ingressando computadores servidores no domínio e fazendo logon](#BKMK_joinlogserver).

Para implantar o DHCP1, que é o computador que executa a função de servidor do protocolo DHCP, conclua estas etapas na seguinte ordem:

- [Instalar o protocolo DHCP](#BKMK_installDHCP)

- [Criar e ativar um novo escopo do DHCP](#BKMK_newscopeDHCP)

> [!NOTE]
> Para executar estes procedimentos usando o Windows PowerShell, abra o PowerShell, digite os cmdlets a seguir em linhas separadas e pressione ENTER. Substitua o nome do escopo, os intervalos de endereços IP iniciais e finais, a máscara de sub-rede e outros valores neste exemplo pelos valores que você deseja usar.
>
> `Install-WindowsFeature DHCP -IncludeManagementTools`
>
> `Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
>
> `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
>
> `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
>
> `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`
>
> `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`
>
> `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`
>
> `Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2`
>
> `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com`

##### <a name="install-dynamic-host-configuration-protocol-dhcp"></a><a name="BKMK_installDHCP"></a>Instalar o protocolo DHCP
Você pode usar este procedimento para instalar e configurar a função de Servidor DHCP usando o Assistente para Adicionar Funções e Recursos.

A associação a **Adminis. do Domínio** ou equivalente é o requisito mínimo para a execução deste procedimento.

###### <a name="to-install-dhcp"></a>Para instalar o DHCP

1.  No DHCP1, no Gerenciador do Servidor, clique em **Gerenciar** e em **Adicionar Funções e Recursos**. O Assistente para Adicionar Funções e Recursos é aberto.

2.  Em **Antes de Começar**, clique em **Avançar**.

    > [!NOTE]
    > A página **Antes de Começar** do Assistente para Adicionar Funções e Recursos não é exibida quando você marca a opção **Ignorar esta página por padrão** quando o Assistente para Funções e Recursos foi executado.

3.  Em **Selecionar Tipo de Instalação**, verifique se **Instalação baseada em função ou recurso** está marcada e clique em **Avançar**.

4.  Em **Selecionar servidor de destino**, verifique se **Selecionar um servidor no pool de servidores** está marcada. Em **Pool de Servidores**, verifique se o computador local está selecionado. Clique em **Avançar**.

5.  Em **selecionar funções de servidor**, em **funções**, selecione **servidor DHCP**. Em **Adicionar recursos que são necessários para Servidor DHCP**, clique em **Adicionar Recursos**. Clique em **Avançar**.

6.  Em **Selecionar recursos**, clique em **Avançar** e, em **Servidor DHCP**, analise as informações fornecidas e clique em **Avançar**.

7.  Em **Confirmar seleções de instalação**, clique em **Reiniciar cada servidor de destino automaticamente, se necessário**. Na solicitação de confirmação dessa seleção, clique em **Sim** e em **Instalar**. A página **progresso da instalação** exibe o status durante o processo de instalação. Quando o processo for concluído, a mensagem "configuração necessária. A instalação bem-sucedida em *ComputerName*"é exibida, em que *ComputerName* é o nome do computador no qual você instalou o servidor DHCP. Na janela de mensagem, clique em **Configuração de DHCP concluída**. O Assistente de configuração pós-instalação do DHCP é aberto. Clique em **Avançar**.

8.  Em **Autorização**, especifique as credenciais que deseja usar para autorizar o servidor DHCP nos Serviços de Domínio Active Directory e clique em **Confirmar**. Na conclusão da autorização, clique em **Fechar**.

##### <a name="create-and-activate-a-new-dhcp-scope"></a><a name="BKMK_newscopeDHCP"></a>Criar e ativar um novo escopo do DHCP
Você pode usar este procedimento para criar um novo escopo do DHCP usando o MMC (Console de Gerenciamento Microsoft) DHCP. Quando você conclui o procedimento, o escopo é ativado e o intervalo de exclusão que você cria impede que o servidor DHCP conceda os endereços IP usados para configurar estaticamente os servidores e outros dispositivos que exigem um endereço IP estático.

A associação em **Administradores DHCP**, ou equivalente, é o requisito mínimo para executar este procedimento.

###### <a name="to-create-and-activate-a-new-dhcp-scope"></a>Para criar e ativar um novo escopo do DHCP

1.  No DHCP1, no Gerenciador do Servidor, clique em **Ferramentas** e em **DHCP**. O MMS DHCP é aberto.

2.  No **DHCP**, expanda o nome do servidor. Por exemplo, se o nome do servidor DHCP for DHCP1.corp.contoso.com, clique na seta para baixo ao lado de **DHCP1.Corp.contoso.com**.

3.  Abaixo do nome do servidor, clique com o botão direito do mouse em **IPv4** e clique em **novo escopo**. O Assistente para Novos Escopos é aberto.

4.  Em **Assistente para Novos Escopos**, clique em **Avançar**.

5.  No **Nome do Escopo**, em **Nome**, digite um nome para o escopo. Por exemplo, digite **Sub-rede 1**.

6.  Em **Descrição**, digite uma descrição para o novo escopo e clique em **Avançar**.

7.  Em **Intervalo de Endereços IP**, faça o seguinte:

    1.  Em **Endereço IP inicial**, digite o endereço IP que é o primeiro no intervalo. Por exemplo, digite **10.0.0.1**.

    2.  Em **Endereço IP final**, digite o endereço IP que é o último no intervalo. Por exemplo, digite **10.0.0.254**. Os valores para **Comprimento** e **Máscara de sub-rede** são inseridos manualmente, com base no endereço IP que você inseriu para o **Endereço IP inicial**.

    3.  Se necessário, modifique os valores em **Comprimento** ou **Máscara de sub-rede**, de forma adequada para seu esquema de endereçamento.

    4.  Clique em **Avançar**.

8.  Em **Adicionar Exclusões**, faça o seguinte:

    1.  Em **Endereço IP inicial**, digite o endereço IP que é o primeiro no intervalo de exclusão. Por exemplo, digite **10.0.0.1**.

    2.  Em **Endereço IP final**, digite o endereço IP que é o último no intervalo de exclusão. Por exemplo, digite **10.0.0.15**.

9. Clique em **Adicionar** e em **Avançar**.

10. Em **Duração da Concessão**, modifique os valores padrão para **Dias**, **Horas** e **Minutos**, de forma adequada para sua rede e clique em **Avançar**.

11. Em **Configurar opções DHCP**, selecione **Sim, desejo configurar essas opções agora** e clique em **Avançar**.

12. Na seção **Roteador (Gateway Padrão)**, siga um destes procedimentos:

    - Se você não tiver roteadores na rede, clique em **Avançar**.

    - No **Endereço IP**, digite o endereço IP do seu gateway padrão ou roteador. Por exemplo, digite **10.0.0.1**. Clique em **Adicionar** e em **Avançar**.

13. Em **Servidor de Nomes de Domínio e DNS**, faça o seguinte:

    1.  Em **Domínio pai**, digite o nome do domínio DNS usado pelos clientes na resolução de nomes. Por exemplo, digite **corp.contoso.com**.

    2.  Em **Nome do servidor**, digite o nome do computador DNS usado pelos clientes na resolução de nomes. Por exemplo, digite **DC1**.

    3.  Clique em **Resolver**. O endereço IP do servidor DNS é adicionado a **Endereço IP**. Clique em **Adicionar**, aguarde a conclusão da validação do endereço IP do servidor DNS e clique em **Avançar**.

14. Em **Servidores WINS**, como você não tem servidores WINS na sua rede, clique em **Avançar**.

15. Em **Ativar Escopo**, selecione **Sim, desejo ativar este escopo agora**.

16. Clique em **Avançar** e em **Concluir**.

> [!IMPORTANT]
> Para criar novos escopos para sub-redes adicionais, repita o procedimento. Use um intervalo de endereços IP diferente para cada sub-rede que você planeja implantar e verifique se o encaminhamento de mensagem DHCP está habilitado em todos os roteadores que levam a outras sub-redes.

### <a name="joining-client-computers-to-the-domain-and-logging-on"></a><a name="BKMK_joinlogclients"></a>Ingressando computadores clientes no domínio e fazendo logon

> [!NOTE]
> Para executar este procedimento usando o Windows PowerShell, abra o PowerShell, digite o cmdlet a seguir e pressione ENTER. Você também deve substituir o nome do domínio pelo nome que deseja usar.
>
> `Add-Computer -DomainName corp.contoso.com`
>
> Quando você for solicitado a fazê-lo, digite o nome de usuário e a senha de uma conta que tenha permissão para ingressar um computador no domínio. Para reiniciar o computador, digite o comando a seguir e pressione ENTER.
>
> `Restart-Computer`

##### <a name="to-join-computers-running-windows-10-to-the-domain"></a>Para unir computadores que executam o Windows 10 ao domínio

1.  Faça logon no computador com a conta de Administrador local.

2.  Em **Pesquisar na Web e no Windows**, digite **System**. Em resultados da pesquisa, clique em **sistema (painel de controle)**. Será exibida a caixa de diálogo **Sistema**.

3.  Em **sistema**, clique em **Configurações avançadas do sistema**. A caixa de diálogo **Propriedades do Sistema** será aberta. Clique na guia **nome do computador** .

4.  Em **nome do computador**, clique em **alterar**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** será aberta.

5.  Em **nome do computador/alterações de domínio** , em **membro de**, clique em **domínio** e digite o nome do domínio que você deseja unir. Por exemplo, se o nome do domínio for corp.contoso.com, digite **corp.contoso.com**.

6.  Clique em **OK**. A caixa de diálogo **Segurança do Windows** será aberta.

7.  Em **Alterações de Nome/Domínio do Computador**, em **Nome de usuário**, digite o nome de usuário, digite a senha no campo **Senha** e clique em **OK**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** é aberta, dando as boas-vindas ao domínio. Clique em **OK**.

8.  A caixa de diálogo **Alterações de Nome/Domínio do Computador** exibe uma mensagem indicando que você deve reiniciar o computador para aplicar as alterações. Clique em **OK**.

9. Na caixa de diálogo **Propriedades do Sistema**, na guia **Nome do Computador**, clique em **Fechar**. A caixa de diálogo **Microsoft Windows** é aberta e exibe uma mensagem, indicando novamente que você deve reiniciar o computador para aplicar as alterações. Clique em **Reiniciar Agora**.

##### <a name="to-join-computers-running-windows-81-to-the-domain"></a>Para unir computadores que executam Windows 8.1 ao domínio

1.  Faça logon no computador com a conta de Administrador local.

2.  Clique com o botão direito do mouse em **Iniciar** e clique em **sistema**. Será exibida a caixa de diálogo **Sistema**.

3.  Em **sistema**, clique em **Configurações avançadas do sistema**. A caixa de diálogo **Propriedades do Sistema** será aberta. Clique na guia **nome do computador** .

4.  Em **nome do computador**, clique em **alterar**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** será aberta.

5.  Em **nome do computador/alterações de domínio** , em **membro de**, clique em **domínio** e digite o nome do domínio que você deseja unir. Por exemplo, se o nome do domínio for corp.contoso.com, digite **corp.contoso.com**.

6.  Clique em **OK**. A caixa de diálogo **Segurança do Windows** será aberta.

7.  Em **Alterações de Nome/Domínio do Computador**, em **Nome de usuário**, digite o nome de usuário, digite a senha no campo **Senha** e clique em **OK**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** é aberta, dando as boas-vindas ao domínio. Clique em **OK**.

8.  A caixa de diálogo **Alterações de Nome/Domínio do Computador** exibe uma mensagem indicando que você deve reiniciar o computador para aplicar as alterações. Clique em **OK**.

9. Na caixa de diálogo **Propriedades do Sistema**, na guia **Nome do Computador**, clique em **Fechar**. A caixa de diálogo **Microsoft Windows** é aberta e exibe uma mensagem, indicando novamente que você deve reiniciar o computador para aplicar as alterações. Clique em **Reiniciar Agora**.

##### <a name="to-log-on-to-the-domain-using-computers-running-windows-10"></a>Para fazer logon no domínio usando computadores que executam o Windows 10

1.  Faça logoff do computador ou o reinicie.

2.  Pressione CTRL + ALT + DELETE. A tela de logon é exibida.

3.  No canto inferior esquerdo, clique em **outro usuário**.

4.  Em **Nome de usuário**, digite o domínio e o nome de usuário no formato *domínio\usuário*. Por exemplo, para fazer logon no domínio corp.contoso.com usando uma conta denominada **User-01**, digite **CORP\User-01**.

5.  Em **Senha**, digite sua senha do domínio e clique na seta ou pressione ENTER.

### <a name="deploying-optional-features-for-network-access-authentication-and-web-services"></a><a name="BKMK_optionalfeatures"></a>Implantando recursos opcionais para a autenticação do acesso à rede e dos serviços Web
Se você pretende implantar servidores de acesso à rede, como pontos de acesso sem fio ou servidores VPN, depois de instalar sua rede principal, é recomendável que você implante um NPS e um servidor Web. Para implantações de acesso à rede, recomendamos o uso de métodos de autenticação baseada em certificado seguro. Você pode usar o NPS para gerenciar políticas de acesso à rede e implantar métodos de autenticação segura. Você pode usar um servidor Web para publicar a CRL (lista de revogação de certificados) de sua autoridade de certificação que fornece os certificados para autenticação segura.

> [!NOTE]
> Você pode implantar certificados de servidor e outros recursos adicionais por meio de Guias Complementares de Rede Principal. Para obter mais informações, consulte [Recursos técnicos adicionais](#BKMK_resources).

A ilustração a seguir mostra a topologia de rede do Windows Server Core com servidores Web e NPS adicionados.

![Topologia de rede do Windows Server Core com servidores Web e NPS adicionados](../media/Core-Network-Guide/cng16_overview_2.jpg)

As seções a seguir fornecem informações sobre como adicionar servidores NPS e Web a sua rede.

- [Implantando o NPS1](#BKMK_deployNPS1)

- [Implantando o WEB1](#BKMK_IIS)

#### <a name="deploying-nps1"></a><a name="BKMK_deployNPS1"></a>Implantando o NPS1
O servidor NPS (Servidor de Políticas de Rede) é instalado como uma etapa preparatória para a implantação de outras tecnologias de acesso à rede, como servidores VPN (rede virtual privada), pontos de acesso sem fio e comutadores de autenticação 802.1X.

O NPS (servidor de diretivas de rede) permite que você configure e gerencie centralmente as políticas de rede com os seguintes recursos: serviço RADIUS (RADIUS) servidor e proxy RADIUS.

O NPS é um componente opcional de uma rede principal, mas você deve instalar o NPS quando qualquer uma das seguintes opções é verdadeira:

- Você está planejando expandir sua rede para incluir servidores de acesso remoto que são compatíveis com o protocolo RADIUS, como um computador executando o Windows Server 2016, o Windows Server 2012 R2, o Windows Server 2012, o Windows Server 2008 R2 ou o Windows Server 2008 e o serviço de roteamento e acesso remoto, gateway de serviços de terminal ou gateway de Área de Trabalho Remota.


- Você planeja implantar a autenticação 802.1 X para acesso com ou sem fio.

Antes de implantar esse serviço de função, você deve executar as etapas a seguir no computador que está configurando como um NPS.

- Siga as etapas na seção [Configurando todos os servidores](#BKMK_configuringAll).

- Siga as etapas na seção [Ingressando computadores servidores no domínio e fazendo logon](#BKMK_joinlogserver).

Para implantar o NPS1, que o computador está executando o serviço de função do NPS (Servidor de Políticas de Rede) da função de servidor de Política de Rede e Serviços de Acesso, conclua esta etapa:

- [Planejando a implantação do NPS1](#bkmk_NetFndtn_Pln_NPS-01)

- [Instalar o NPS (Servidor de Políticas de Rede)](#BKMK_installNPS)

- [Registrar o NPS no domínio padrão](#BKMK_registerNPS)

> [!NOTE]
> Este guia fornece instruções para implantar o NPS em um servidor autônomo ou VM chamada NPS1.  Outro modelo de implantação recomendado é a instalação do NPS em um controlador de domínio. Se preferir instalar o NPS em um controlador de domínio em vez de em um servidor autônomo, instale o NPS no DC1.

##### <a name="planning-the-deployment-of-nps1"></a><a name="bkmk_NetFndtn_Pln_NPS-01"></a>Planejando a implantação do NPS1
Se você pretende implantar servidores de acesso à rede, como pontos de acesso sem fio ou servidores VPN, depois de implantar a rede principal, recomendamos que implante o NPS.

Quando você usa o NPS como um servidor do serviço RADIUS, o NPS executa a autenticação e a autorização para solicitações de conexão por meio de servidores de acesso à rede. O NPS também permite que você configure e gerencie de forma centralizada as políticas de rede que determinam quem pode acessar a rede, como eles podem acessar a rede e quando eles podem acessar a rede.

Estas são as principais etapas de planejamento antes de instalar o NPS.

- Planeje o banco de dados de contas de usuário. Por padrão, se você ingressar o servidor que executa o NPS em um domínio do Active Directory, o NPS executará a autenticação e a autorização usando o banco de dados de contas de usuário do AD DS. Em alguns casos, como em grandes redes que usam o NPS como um proxy RADIUS para encaminhar solicitações de conexão a outros servidores RADIUS, você pode desejar instalar o NPS em um computador que não é membro do domínio.

- Planeje a contabilização do RADIUS. O NPS permite que você registre em log os dados de contabilização em um banco de dados SQL Server ou em um arquivo de texto no computador local. Se você deseja usar o registro em log do SQL Server, planeje a instalação e a configuração de seu servidor que executa o SQL Server.

##### <a name="install-network-policy-server-nps"></a><a name="BKMK_installNPS"></a>Instalar o NPS (Servidor de Políticas de Rede)
Você pode usar este procedimento para instalar o NPS (servidor de diretivas de rede) usando o assistente para adicionar funções e recursos. O NPS é um serviço de função da função de servidor Serviços de Acesso e Política de Rede.

> [!NOTE]
> Por padrão, o NPS ouve o tráfego RADIUS nas portas 1812, 1813, 1645 e 1646 em todos os adaptadores de rede instalados. Se o Firewall do Windows com segurança avançada estiver habilitado quando você instalar o NPS, as exceções de firewall para essas portas serão criadas automaticamente durante o processo de instalação para o \( tráfego IPv6 e IPv4 do protocolo IP versão 6 \) . Se os servidores de acesso à rede estiverem configurados para enviar tráfego RADIUS por portas diferentes desses padrões, remova as exceções criadas no firewall do Windows com segurança avançada durante a instalação do NPS e crie exceções para as portas que você usa para o tráfego RADIUS.

**Credenciais administrativas**

Para concluir este procedimento, você deve ser um membro do grupo **Administradores de Domínio**.

> [!NOTE]
> Para executar este procedimento usando o Windows PowerShell, abra o PowerShell, digite o texto a seguir e pressione ENTER.
>
> `Install-WindowsFeature NPAS -IncludeManagementTools`

###### <a name="to-install-nps"></a>Para instalar o NPS

1.  No NPS1, no Gerenciador do Servidor, clique em **Gerenciar** e em **Adicionar Funções e Recursos**. O Assistente para Adicionar Funções e Recursos é aberto.

2.  Em **Antes de Começar**, clique em **Avançar**.

    > [!NOTE]
    > A página **Antes de Começar** do Assistente para Adicionar Funções e Recursos não é exibida quando você marca a opção **Ignorar esta página por padrão** quando o Assistente para Funções e Recursos foi executado.

3.  Em **Selecionar Tipo de Instalação**, verifique se **Instalação baseada em função ou recurso** está marcada e clique em **Avançar**.

4.  Em **Selecionar servidor de destino**, verifique se **Selecionar um servidor no pool de servidores** está marcada. Em **Pool de Servidores**, verifique se o computador local está selecionado. Clique em **Avançar**.

5.  Em **selecionar funções de servidor**, em **funções**, selecione **serviços de acesso e política de rede**. Uma caixa de diálogo será aberta perguntando se ele deve adicionar recursos necessários para serviços de acesso e política de rede. Clique em **Adicionar Recursos** e depois em **Avançar**.

6.  Em **Selecionar recursos**, clique em **Avançar** e, em **Serviços de Acesso e Política de Rede**, analise as informações fornecidas e clique em **Avançar**.

7.  Em **Selecionar serviços de função**, clique em **Servidor de Políticas de Rede**.  Em **Adicionar recursos que são necessários para Servidor de Políticas de Rede**, clique em **Adicionar Recursos**. Clique em **Avançar**.

8.  Em **Confirmar seleções de instalação**, clique em **Reiniciar cada servidor de destino automaticamente, se necessário**. Na solicitação de confirmação dessa seleção, clique em **Sim** e em **Instalar**. A página Progresso da instalação exibe o status durante o processo de instalação. Quando o processo for concluído, a mensagem "a instalação foi bem-sucedida em *ComputerName*" será exibida, em que *ComputerName* é o nome do computador no qual você instalou o servidor de políticas de rede. Clique em **fechar**

##### <a name="register-the-nps-in-the-default-domain"></a><a name="BKMK_registerNPS"></a>Registrar o NPS no domínio padrão
Você pode usar este procedimento para registrar um NPS no domínio em que o servidor é membro do domínio.

NPSs deve ser registrado em Active Directory para que eles tenham permissão para ler as propriedades de discagem de contas de usuário durante o processo de autorização. O registro de um NPS adiciona o servidor ao grupo de **Servidores RAS e ias** em Active Directory.

**Credenciais administrativas**

Para concluir este procedimento, você deve ser um membro do grupo **Administradores de Domínio**.

> [!NOTE]
> Para executar esse procedimento usando comandos do Shell de rede (netsh) no Windows PowerShell, abra o PowerShell e digite o seguinte e pressione ENTER.
>
> `netsh nps add registeredserver domain=corp.contoso.com server=NPS1.corp.contoso.com`

###### <a name="to-register-an-nps-in-its-default-domain"></a>Para registrar um NPS em seu domínio padrão

1.  No NPS1, no Gerenciador do Servidor, clique em Ferramentas e em **Servidor de Políticas de Rede**. O MMC Servidor de Políticas de Rede é aberto.

2.  Clique com o botão direito do mouse em **NPS (Local)** e clique em **Registrar servidor no Active Directory**. A caixa de diálogo **Servidor de Políticas de Rede** é aberta.

3.  Em **Servidor de Políticas de Rede**, clique em **OK** e em **OK** novamente.

Para obter mais informações sobre o servidor de políticas de rede, consulte [servidor de diretivas de rede (NPS)](../technologies/nps/nps-top.md).

#### <a name="deploying-web1"></a><a name="BKMK_IIS"></a>Implantando o WEB1

A função do servidor Web (IIS) no Windows Server 2016 fornece uma plataforma segura, fácil de gerenciar, modular e extensível para hospedagem confiável de sites, serviços e aplicativos. Com o Serviços de Informações da Internet (IIS), você pode compartilhar informações com usuários na Internet, em uma intranet ou em uma extranet. O IIS é uma plataforma Web unificada que integra IIS, ASP.NET, serviços FTP, PHP e Windows Communication Foundation (WCF).

Além de permitir que você publique uma CRL para acesso por computadores membros do domínio, a função de servidor servidor Web (IIS) permite que você configure e gerencie vários sites da Web, aplicativos Web e sites FTP. O IIS também oferece os seguintes benefícios:

- Maximizar a segurança da Web através de uma estrutura menor de servidores e isolamento automático de aplicativos.

- Implantar e executar facilmente aplicativos Web em ASP.NET, ASP clássico e PHP no mesmo servidor.

- Obter o isolamento do aplicativo dando aos processos de trabalho uma identidade exclusiva e configuração de área restrita por padrão, reduzindo ainda mais os riscos de segurança.

- Adicionar, remover e até mesmo substituir facilmente componentes internos do IIS por módulos personalizados, adaptados às necessidades dos clientes.

- Acelerar o seu site através de armazenamento em cache dinâmico interno e compactação aprimorada.

Para implantar o WEB1, que é o computador que está executando a função de servidor Servidor Web (IIS), faça o seguinte:

- Siga as etapas na seção [Configurando todos os servidores](#BKMK_configuringAll).

- Siga as etapas na seção [Ingressando computadores servidores no domínio e fazendo logon](#BKMK_joinlogserver).

- [Instalar a função de servidor do Servidor Web (IIS)](#BKMK_install_IIS)

##### <a name="install-the-web-server-iis-server-role"></a><a name="BKMK_install_IIS"></a>Instalar a função de servidor do Servidor Web (IIS)
Para concluir este procedimento, é preciso ser um membro do grupo **Administradores**.

> [!NOTE]
> Para executar este procedimento usando o Windows PowerShell, abra o PowerShell, digite o texto a seguir e pressione ENTER.
>
> `Install-WindowsFeature Web-Server -IncludeManagementTools`

1.  No **Gerenciador do Servidor**, clique em **Gerenciar** e depois em **Adicionar Funções e Recursos**. O Assistente para Adicionar Funções e Recursos é aberto.

2.  Em **Antes de Começar**, clique em **Avançar**.

    > [!NOTE]
    > A página **Antes de Começar** do Assistente para Adicionar Funções e Recursos não é exibida quando você marca a opção **Ignorar esta página por padrão** quando o Assistente para Funções e Recursos foi executado.

3.  Na página **Selecionar tipo de instalação** , clique em **Avançar**.

4.  Na página **selecionar servidor de destino** , verifique se o computador local está selecionado e clique em **Avançar**.

5.  Na página **selecionar funções de servidor** , role para e selecione **servidor Web (IIS)**. A caixa de diálogo **Adicionar recursos necessários para o servidor Web (IIS)** é aberta. Clique em **Adicionar Recursos** e depois em **Avançar**.

6.  Clique em **Avançar** até ter aceitado todas as configurações padrão do servidor Web e clique em **Instalar**.

7.  Confirme se todas as instalações tiveram êxito e clique em **Fechar**.

## <a name="additional-technical-resources"></a><a name="BKMK_resources"></a>Recursos técnicos adicionais
Para obter mais informações sobre as tecnologias neste guia, consulte os recursos a seguir:

 Recursos de biblioteca técnica do Windows Server 2016, Windows Server 2012 R2 e Windows Server 2012

- [O que há de novo no Active Directory Domain Services (AD DS) no Windows Server 2016](../../identity/whats-new-active-directory-domain-services.md)

- [Active Directory Domain Services visão geral](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831484(v=ws.11)) em https://technet.microsoft.com/library/hh831484.aspx .

- [Visão geral do DNS (sistema de nomes de domínio)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831667(v=ws.11)) em https://technet.microsoft.com/library/hh831667.aspx .

- [Implementando a função Administradores de DNS](/previous-versions/windows/it-pro/windows-server-2003/cc756152(v=ws.10))

- [Visão geral do protocolo DHCP](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831825(v=ws.11)) em https://technet.microsoft.com/library/hh831825.aspx .

- [Visão geral dos serviços de acesso e política de rede](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)) em https://technet.microsoft.com/library/hh831683.aspx .

- [Visão geral do servidor Web (IIS)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831725(v=ws.11)) em https://technet.microsoft.com/library/hh831725.aspx .

## <a name="appendices-a-through-e"></a><a name="BKMK_appendix"></a>Apêndices A a E
As seções a seguir contêm informações de configuração adicionais para computadores que executam sistemas operacionais diferentes do Windows Server 2016, Windows 10, Windows Server 2012 e Windows 8. Além disso, uma planilha de preparação de rede é fornecida para ajudá-lo com sua implantação.

1.  [Apêndice A – Renomeando computadores](#BKMK_A)

2.  [Apêndice B – Configurando endereços IP estáticos](#BKMK_B)

3.  [Apêndice C – unindo computadores ao domínio](#BKMK_C)

4.  [Apêndice D – fazer logon no domínio](#BKMK_D)

5.  [Apêndice E – Folha de preparação do planejamento da Rede Principal](#BKMK_E)

## <a name="appendix-a---renaming-computers"></a><a name="BKMK_A"></a>Apêndice A – Renomeando computadores
Você pode usar os procedimentos nesta seção para fornecer computadores que executam o Windows Server 2008 R2, Windows 7, Windows Server 2008 e Windows Vista com um nome de computador diferente.

- [Windows Server 2008 R2 e Windows 7](#bkmk_NetFndtn_Pln_rename_R2)

- [Windows Server 2008 e Windows Vista](#bkmk_NetFndtn_Pln_Renam08)

### <a name="windows-server-2008-r2-and-windows-7"></a><a name="bkmk_NetFndtn_Pln_rename_R2"></a>Windows Server 2008 R2 e Windows 7
A associação a **Administradores** ou equivalente é o requisito mínimo para a execução destes procedimentos.

##### <a name="to-rename-computers-running-windows-server-2008-r2-and-windows-7"></a>Para renomear os computadores que executam o Windows Server 2008 R2 e o Windows 7

1.  Clique em **Iniciar**, clique com botão direito do **computador** e clique em **Propriedades**. Será exibida a caixa de diálogo **Sistema**.

2.  Em **Nome do computador, domínio e configurações de grupo de trabalho**, clique em **Alterar configurações**. A caixa de diálogo **Propriedades do Sistema** será aberta.

    > [!NOTE]
    > Em computadores que executam o Windows 7, antes da caixa de diálogo **Propriedades do sistema** ser aberta, a caixa de diálogo controle de **conta de usuário** é aberta, solicitando permissão para continuar. Clique em **Continuar** para prosseguir.

3.  Clique em **Alterar**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** será aberta.

4.  Em **Nome do Computador**, digite o nome do seu computador. Por exemplo, se você deseja denominar o computador como DC1, digite **DC1**.

5.  Clique em **OK** duas vezes, clique em **Fechar** e depois em **Reiniciar Agora** para reiniciar o computador.

### <a name="windows-server-2008-and-windows-vista"></a><a name="bkmk_NetFndtn_Pln_Renam08"></a>Windows Server 2008 e Windows Vista
A associação a **Administradores** ou equivalente é o requisito mínimo para a execução destes procedimentos.

##### <a name="to-rename-computers-running-windows-server-2008-and-windows-vista"></a>Para renomear os computadores executando o Windows Server 2008 e o Windows Vista

1.  Clique em **Iniciar**, clique com botão direito do **computador** e clique em **Propriedades**. Será exibida a caixa de diálogo **Sistema**.

2.  Em **Nome do computador, domínio e configurações de grupo de trabalho**, clique em **Alterar configurações**. A caixa de diálogo **Propriedades do Sistema** será aberta.

    > [!NOTE]
    > Em computadores que executam o Windows Vista, antes da caixa de diálogo **Propriedades do sistema** ser aberta, a caixa de diálogo controle de **conta de usuário** é aberta, solicitando permissão para continuar. Clique em **Continuar** para prosseguir.

3.  Clique em **Alterar**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** será aberta.

4.  Em **Nome do Computador**, digite o nome do seu computador. Por exemplo, se você deseja denominar o computador como DC1, digite **DC1**.

5.  Clique em **OK** duas vezes, clique em **Fechar** e depois em **Reiniciar Agora** para reiniciar o computador.

## <a name="appendix-b---configuring-static-ip-addresses"></a><a name="BKMK_B"></a>Apêndice B – Configurando endereços IP estáticos
Este tópico fornece procedimentos para configurar endereços IP estáticos em computadores que executam os seguintes sistemas operacionais:

- [Windows Server 2008 R2](#bkmk_R2Cng_WS08R2IP)

- [Windows Server 2008](#bkmk_NetFndtn_Pln_CfgStatic08)

### <a name="windows-server-2008-r2"></a><a name="bkmk_R2Cng_WS08R2IP"></a>Windows Server 2008 R2
A associação em **Administradores**, ou equivalente, é o requisito mínimo para executar este procedimento.

##### <a name="to-configure-a-static-ip-address-on-a-computer-running-windows-server-2008-r2"></a>Para configurar um endereço IP estático em um computador executando o Windows Server 2008 R2

1.  Clique em **Iniciar** e em **Painel de Controle**.

2.  Em **Painel de Controle**, clique em **Rede e Internet**. A janela **Rede e Internet** será aberta.

    Em **Rede e Internet**, clique em **Central de Rede e Compartilhamento**. A **Central de Rede e Compartilhamento** será aberta.

3.  Na **Central de Rede e Compartilhamento**, clique em **Alterar as configurações do adaptador**. A janela **Conexões de Rede** será aberta.

4.  Em **Conexões de Rede**, clique com o botão direito na conexão de rede que deseja configurar e clique em **Propriedades**.

5.  Em **Propriedades da Conexão Local**, em **Esta conexão utiliza os seguintes itens**, selecione **Protocolo TCP/IPv4 (TCP/IP Versão 4)** e clique em **Propriedades**. A caixa de diálogo **Propriedades do Protocolo TCP/IPv4 (TCP/IP Versão 4)** será aberta.

6.  Em **Propriedades do Protocolo TCP/IPv4 (TCP/IP Versão 4)**, na guia **Geral**, clique em **Usar o seguinte endereço IP**. Em **Endereço IP**, digite o endereço IP que deseja usar.

7.  Pressione Tab para colocar o cursor em **Máscara de sub-rede**. Um valor padrão para máscara de sub-rede será inserido automaticamente. Aceite a máscara de sub-rede padrão ou digite a máscara de sub-rede que deseja usar.

8.  No **Gateway padrão**, digite o endereço IP do seu gateway padrão.

9. Em **Servidor DNS preferencial**, digite o endereço IP do seu servidor DNS. Se você planeja usar o computador local como o servidor DNS preferencial, digite o endereço IP do computador local.

10. Em **Servidor DNS alternativo**, digite o endereço IP do seu servidor DNS alternativo, se houver. Se você planeja usar o computador local como um servidor DNS alternativo, digite o endereço IP do computador local.

11. Clique em **OK** e então clique em **Fechar**.

### <a name="windows-server-2008"></a><a name="bkmk_NetFndtn_Pln_CfgStatic08"></a>Windows Server 2008
A associação a **Administradores** ou equivalente é o requisito mínimo para a execução destes procedimentos.

##### <a name="to-configure-a-static-ip-address-on-a-computer-running-windows-server-2008"></a>Para configurar um endereço IP estático em um computador executando o Windows Server 2008

1.  Clique em **Iniciar** e em **Painel de Controle**.

2.  No **Painel de Controle**, selecione o **Modo de Exibição Clássico** e clique duas vezes em **Central de Rede e Compartilhamento**.

3.  Na **Central de Rede e Compartilhamento**, em **Tarefas**, clique em **Gerenciar Conexões de Rede**.

4.  Em **Conexões de Rede**, clique com o botão direito na conexão de rede que deseja configurar e clique em **Propriedades**.

5.  Em **Propriedades da Conexão Local**, em **Esta conexão utiliza os seguintes itens**, selecione **Protocolo TCP/IPv4 (TCP/IP Versão 4)** e clique em **Propriedades**. A caixa de diálogo **Propriedades do Protocolo TCP/IPv4 (TCP/IP Versão 4)** será aberta.

6.  Em **Propriedades do Protocolo TCP/IPv4 (TCP/IP Versão 4)**, na guia **Geral**, clique em **Usar o seguinte endereço IP**. Em **Endereço IP**, digite o endereço IP que deseja usar.

7.  Pressione Tab para colocar o cursor em **Máscara de sub-rede**. Um valor padrão para máscara de sub-rede será inserido automaticamente. Aceite a máscara de sub-rede padrão ou digite a máscara de sub-rede que deseja usar.

8.  No **Gateway padrão**, digite o endereço IP do seu gateway padrão.

9. Em **Servidor DNS preferencial**, digite o endereço IP do seu servidor DNS. Se você planeja usar o computador local como o servidor DNS preferencial, digite o endereço IP do computador local.

10. Em **Servidor DNS alternativo**, digite o endereço IP do seu servidor DNS alternativo, se houver. Se você planeja usar o computador local como um servidor DNS alternativo, digite o endereço IP do computador local.

11. Clique em **OK** e então clique em **Fechar**.

## <a name="appendix-c---joining-computers-to-the-domain"></a><a name="BKMK_C"></a>Apêndice C – unindo computadores ao domínio
Você pode usar esses procedimentos para unir computadores que executam o Windows Server 2008 R2, Windows 7, Windows Server 2008 e Windows Vista ao domínio.

- [Windows Server 2008 R2 e Windows 7](#BKMK_c1)

- [Windows Server 2008 e Windows Vista](#BKMK_c2)

> [!IMPORTANT]
> Para ingressar um computador em um domínio, faça logon no computador com a conta de Administrador local ou, se já estiver conectado ao computador com uma conta de usuário que não tem credenciais administrativas do computador local, forneça as credenciais para a conta de Administrador local durante o processo de ingressar o computador no domínio. Além disso, você deve ter uma conta de usuário no domínio no qual deseja ingressar o computador. Durante o processo de ingressar o computador no domínio, você será solicitado para inserir as credenciais de conta de domínio (nome de usuário e senha).

### <a name="windows-server-2008-r2-and-windows-7"></a><a name="BKMK_c1"></a>Windows Server 2008 R2 e Windows 7
O requisito mínimo para executar este procedimento é a associação ao grupo **Usuários do Domínio** ou equivalente.

##### <a name="to-join-computers-running-windows-server-2008-r2-and-windows-7-to-the-domain"></a>Para ingressar computadores que executam o Windows Server 2008 R2 e o Windows 7 no domínio

1.  Faça logon no computador com a conta de Administrador local.

2.  Clique em **Iniciar**, clique com botão direito do **computador** e clique em **Propriedades**. Será exibida a caixa de diálogo **Sistema**.

3.  Em **Nome do computador, domínio e configurações de grupo de trabalho**, clique em **Alterar configurações**. A caixa de diálogo **Propriedades do Sistema** será aberta.

    > [!NOTE]
    > Em computadores que executam o Windows 7, antes da caixa de diálogo **Propriedades do sistema** ser aberta, a caixa de diálogo controle de **conta de usuário** é aberta, solicitando permissão para continuar. Clique em **Continuar** para prosseguir.

4.  Clique em **Alterar**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** será aberta.

5.  No **Nome do Computador**, em **Membro de**, selecione **Domínio** e digite o nome do domínio no qual você deseja ingressar. Por exemplo, se o nome do domínio for corp.contoso.com, digite **corp.contoso.com**.

6.  Clique em **OK**. A caixa de diálogo **Segurança do Windows** será aberta.

7.  Em **Alterações de Nome/Domínio do Computador**, em **Nome de usuário**, digite o nome de usuário, digite a senha no campo **Senha** e clique em **OK**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** é aberta, dando as boas-vindas ao domínio. Clique em **OK**.

8.  A caixa de diálogo **Alterações de Nome/Domínio do Computador** exibe uma mensagem indicando que você deve reiniciar o computador para aplicar as alterações. Clique em **OK**.

9. Na caixa de diálogo **Propriedades do Sistema**, na guia **Nome do Computador**, clique em **Fechar**. A caixa de diálogo **Microsoft Windows** é aberta e exibe uma mensagem, indicando novamente que você deve reiniciar o computador para aplicar as alterações. Clique em **Reiniciar Agora**.

### <a name="windows-server-2008-and-windows-vista"></a><a name="BKMK_c2"></a>Windows Server 2008 e Windows Vista
O requisito mínimo para executar este procedimento é a associação ao grupo **Usuários do Domínio** ou equivalente.

##### <a name="to-join-computers-running-windows-server-2008-and-windows-vista-to-the-domain"></a>Para ingressar computadores que executam o Windows Server 2008 e o Windows Vista no domínio

1.  Faça logon no computador com a conta de Administrador local.

2.  Clique em **Iniciar**, clique com botão direito do **computador** e clique em **Propriedades**. Será exibida a caixa de diálogo **Sistema**.

3.  Em **Nome do computador, domínio e configurações de grupo de trabalho**, clique em **Alterar configurações**. A caixa de diálogo **Propriedades do Sistema** será aberta.

4.  Clique em **Alterar**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** será aberta.

5.  No **Nome do Computador**, em **Membro de**, selecione **Domínio** e digite o nome do domínio no qual você deseja ingressar. Por exemplo, se o nome do domínio for corp.contoso.com, digite **corp.contoso.com**.

6.  Clique em **OK**. A caixa de diálogo **Segurança do Windows** será aberta.

7.  Em **Alterações de Nome/Domínio do Computador**, em **Nome de usuário**, digite o nome de usuário, digite a senha no campo **Senha** e clique em **OK**. A caixa de diálogo **Alterações de Nome/Domínio do Computador** é aberta, dando as boas-vindas ao domínio. Clique em **OK**.

8.  A caixa de diálogo **Alterações de Nome/Domínio do Computador** exibe uma mensagem indicando que você deve reiniciar o computador para aplicar as alterações. Clique em **OK**.

9. Na caixa de diálogo **Propriedades do Sistema**, na guia **Nome do Computador**, clique em **Fechar**. A caixa de diálogo **Microsoft Windows** é aberta e exibe uma mensagem, indicando novamente que você deve reiniciar o computador para aplicar as alterações. Clique em **Reiniciar Agora**.

## <a name="appendix-d---log-on-to-the-domain"></a><a name="BKMK_D"></a>Apêndice D – fazer logon no domínio
Você pode usar esses procedimentos para fazer logon no domínio usando computadores que executam o Windows Server 2008 R2, o Windows 7, o Windows Server 2008 e o Windows Vista.

- [Windows Server 2008 R2 e Windows 7](#BKMK_d1)

- [Windows Server 2008 e Windows Vista](#BKMK_d2)

### <a name="windows-server-2008-r2-and-windows-7"></a><a name="BKMK_d1"></a>Windows Server 2008 R2 e Windows 7
O requisito mínimo para executar este procedimento é a associação ao grupo **Usuários do Domínio** ou equivalente.

##### <a name="log-on-to-the-domain-using-computers-running-windows-server-2008-r2-and-windows-7"></a>Fazer logon no domínio usando computadores que executam o Windows Server 2008 R2 e o Windows 7

1.  Faça logoff do computador ou o reinicie.

2.  Pressione CTRL + ALT + DELETE. A tela de logon é exibida.

3.  Clique em **Trocar de Usuário** e em **Outro Usuário**.

4.  Em **Nome de usuário**, digite o domínio e o nome de usuário no formato *domínio\usuário*. Por exemplo, para fazer logon no domínio corp.contoso.com usando uma conta denominada **User-01**, digite **CORP\User-01**.

5.  Em **Senha**, digite sua senha do domínio e clique na seta ou pressione ENTER.

### <a name="windows-server-2008-and-windows-vista"></a><a name="BKMK_d2"></a>Windows Server 2008 e Windows Vista
O requisito mínimo para executar este procedimento é a associação ao grupo **Usuários do Domínio** ou equivalente.

##### <a name="log-on-to-the-domain-using-computers-running-windows-server-2008-and-windows-vista"></a>Fazer logon no domínio usando computadores que executam o Windows Server 2008 e o Windows Vista

1.  Faça logoff do computador ou o reinicie.

2.  Pressione CTRL + ALT + DELETE. A tela de logon é exibida.

3.  Clique em **Trocar de Usuário** e em **Outro Usuário**.

4.  Em **Nome de usuário**, digite o domínio e o nome de usuário no formato *domínio\usuário*. Por exemplo, para fazer logon no domínio corp.contoso.com usando uma conta denominada **User-01**, digite **CORP\User-01**.

5.  Em **Senha**, digite sua senha do domínio e clique na seta ou pressione ENTER.

## <a name="appendix-e---core-network-planning-preparation-sheet"></a><a name="BKMK_E"></a>Apêndice E – Folha de preparação do planejamento da Rede Principal
Você pode usar esta Folha de preparação do planejamento de Rede Principal para obter as informações necessárias para instalar uma rede principal. Este tópico fornece as tabelas que contêm os itens de configuração individual para cada computador do servidor para o qual você deve fornecer informações ou valores específicos durante o processo de instalação ou configuração. Os valores de exemplo são fornecidos para cada item de configuração.

Para fins de planejamento e acompanhamento, os espaços são fornecidos em cada tabela para você inserir os valores usados para sua implantação. Se você se registrar em log os valores relacionados com a segurança nessas tabelas, deverá armazenar as informações em um local seguro.

Estes links levam para as seções neste tópico que fornecem itens de configuração e exemplos de valores que estão associados com os procedimentos de implantação apresentados neste guia.

1.  [Instalando os Serviços de Domínio Active Directory e o DNS](#BKMK_FndtnPrep_InstallAD)

    - [Configurando uma zona de pesquisa inversa de DNS](#BKMK_FndtnPrep_DNSRevrsLook)

2.  [Instalando o DHCP](#BKMK_FndtnPrep_InstallDHCP)

    - [Criando um intervalo de exclusão no DHCP](#BKMK_FndtnPrep_DHCP_Exclusn)

    - [Criando um novo escopo do DHCP](#bkmk_NetFndtn_Pln_DHCP_NewScope)

3.  [Instalando o Servidor de Políticas de Rede (opcional)](#BKMK_FndtnPrep_InstallNPS)

### <a name="installing-active-directory-domain-services-and-dns"></a><a name="BKMK_FndtnPrep_InstallAD"></a>Instalando os Serviços de Domínio Active Directory e o DNS
As tabelas nesta seção listam os itens de configuração para a pré-instalação e a instalação do AD DS (Serviços de Domínio Active Directory) e do DNS.

##### <a name="pre-installation-configuration-items-for-ad-ds-and-dns"></a>Itens de configuração de pré-instalação para o AD DS e o DNS
As seguintes tabelas listam os itens de configuração de pré-instalação descritos em [Configurando todos os servidores](#BKMK_configuringAll):

- [Configurar um endereço IP estático](#BKMK_ip)

|Itens de configuração|Valores de exemplo|Valores|
|-----------------------|------------------|----------|
|Endereço IP|10.0.0.2||
|Máscara de sub-rede|255.255.255.0||
|Gateway padrão|10.0.0.1||
|Servidor DNS preferencial|127.0.0.1||
|Servidor DNS alternativo|10.0.0.15||

- [Renomear o computador](#BKMK_rename)

|Item de configuração|Valor de exemplo|Valor|
|----------------------|-----------------|---------|
|Nome do computador|DC1||

##### <a name="ad-ds-and-dns-installation-configuration-items"></a>Itens de configuração de instalação do AD DS e do DNS
Itens de configuração para o procedimento de implantação da Rede Principal do Windows Server [Instalar o AD DS e o DNS para uma Nova Floresta](#BKMK_installAD-DNS):

|Itens de configuração|Valores de exemplo|Valores|
|-----------------------|------------------|----------|
|Nome DNS completo|corp.contoso.com||
|Nível funcional da floresta|Windows Server 2003||
|Local da pasta do banco de dados dos Serviços de Domínio Active Directory|E:\Configuration\\<p>Ou aceite o local padrão.||
|Local da pasta dos arquivos de log dos Serviços de Domínio Active Directory|E:\Configuration\\<p>Ou aceite o local padrão.||
|Local da pasta do SYSVOL dos Serviços de Domínio Active Directory|E:\Configuration\\<p>Ou aceite o local padrão.||
|Senha do Administrador do Modo de Restauração de Diretório|J*p2leO4$F||
|Nome de arquivo de resposta (opcional)|AD DS_AnswerFile||

#### <a name="configuring-a-dns-reverse-lookup-zone"></a><a name="BKMK_FndtnPrep_DNSRevrsLook"></a>Configurando uma zona de pesquisa inversa de DNS

|Itens de configuração|Valores de exemplo|Valores|
|-----------------------|------------------|----------|
|Tipo de zona:|-Zona primária<br />-Zona secundária<br />-Zona de stub||
|Tipo de zona<p>**Armazenar a zona no Active Directory**|-Selecionado<br />-Não selecionado||
|Escopo de replicação de zona do Active Directory|-Para todos os servidores DNS nesta floresta<br />-Para todos os servidores DNS neste domínio<br />-Para todos os controladores de domínio neste domínio<br />-Para todos os controladores de domínio especificados no escopo desta partição de diretório||
|Nome da zona de pesquisa inversa<p>(tipo de IP)|-Zona de pesquisa inversa de IPv4<br />-Zona de pesquisa inversa do IPv6||
|Nome da zona de pesquisa inversa<p>(ID da rede)|10.0.0||

### <a name="installing-dhcp"></a><a name="BKMK_FndtnPrep_InstallDHCP"></a>Instalando o DHCP
As tabelas nesta seção listam os itens de configuração de pré-instalação e de instalação do DHCP.

##### <a name="pre-installation-configuration-items-for-dhcp"></a>Itens de configuração de pré-instalação do DHCP
As seguintes tabelas listam os itens de configuração de pré-instalação descritos em [Configurando todos os servidores](#BKMK_configuringAll):

- [Configurar um endereço IP estático](#BKMK_ip)

|Itens de configuração|Valores de exemplo|Valores|
|-----------------------|------------------|----------|
|Endereço IP|10.0.0.3||
|Máscara de sub-rede|255.255.255.0||
|Gateway padrão|10.0.0.1||
|Servidor DNS preferencial|10.0.0.2||
|Servidor DNS alternativo|10.0.0.15||

- [Renomear o computador](#BKMK_rename)

|Item de configuração|Valor de exemplo|Valor|
|----------------------|-----------------|---------|
|Nome do computador|DHCP1||

##### <a name="dhcp-installation-configuration-items"></a>Itens de configuração de instalação do DHCP
Os itens de configuração do procedimento de implantação da Rede Principal do Windows Server [Instalar o protocolo DHCP](#BKMK_installDHCP):

|Itens de configuração|Valores de exemplo|Valores|
|-----------------------|------------------|----------|
|Ligações de conexão de rede|Ethernet||
|Configurações do servidor DNS|DC1||
|Endereço IP do servidor DNS preferencial|10.0.0.2||
|Endereço IP do servidor DNS alternativo|10.0.0.15||
|Nome do escopo|Corp1||
|Endereço IP inicial|10.0.0.1||
|Endereço IP final|10.0.0.254||
|Máscara de sub-rede|255.255.255.0||
|Gateway padrão (opcional)|10.0.0.1||
|Duração da concessão|8 dias||
|Modo de operação do servidor DHCP IPv6|não ativado||

#### <a name="creating-an-exclusion-range-in-dhcp"></a><a name="BKMK_FndtnPrep_DHCP_Exclusn"></a>Criando um intervalo de exclusão no DHCP
Itens de configuração para criar um intervalo de exclusão durante a criação de um escopo no DHCP.

|Itens de configuração|Valores de exemplo|Valores|
|-----------------------|------------------|----------|
|Nome do escopo|Corp1||
|Descrição do escopo|Sub-rede do escritório principal 1||
|Endereço IP inicial do intervalo de exclusão|10.0.0.1||
|Endereço IP final do intervalo de exclusão|10.0.0.15||

#### <a name="creating-a-new-dhcp-scope"></a><a name="bkmk_NetFndtn_Pln_DHCP_NewScope"></a>Criando um novo escopo do DHCP
Os itens de configuração do procedimento de implantação da Rede Principal do Windows Server [Criar e ativar um novo escopo do DHCP](#BKMK_newscopeDHCP):

|Itens de configuração|Valores de exemplo|Valores|
|-----------------------|------------------|----------|
|Novo nome do escopo|Corp2||
|Descrição do escopo|Sub-rede principal do escritório 2||
|(intervalo de endereços IP)<p>Endereço IP inicial|10.0.1.1||
|(intervalo de endereços IP)<p>Endereço IP final|10.0.1.254||
|Comprimento|8||
|Máscara de sub-rede|255.255.255.0||
|Endereço IP Inicial (intervalo de exclusão)|10.0.1.1||
|Endereço IP final do intervalo de exclusão|10.0.1.15||
|Duração da concessão<p>Dias<p>Horas<p>minutos|-8<br />-0<br />-0||
|Roteador (gateway padrão)<p>Endereço IP|10.0.1.1||
|Domínio pai DNS|corp.contoso.com||
|Servidor DNS<p>Endereço IP|10.0.0.2||

### <a name="installing-network-policy-server-optional"></a><a name="BKMK_FndtnPrep_InstallNPS"></a>Instalando o Servidor de Políticas de Rede (opcional)
As tabelas nesta seção listam os itens de configuração de pré-instalação e de instalação do NPS.

##### <a name="pre-installation-configuration-items"></a>Itens de configuração de pré-instalação
As seguintes três tabelas listam os itens de configuração de pré-instalação descritos em [Configurando todos os servidores](#BKMK_configuringAll):

- [Configurar um endereço IP estático](#BKMK_ip)

|Itens de configuração|Valores de exemplo|Valores|
|-----------------------|------------------|----------|
|Endereço IP|10.0.0.4||
|Máscara de sub-rede|255.255.255.0||
|Gateway padrão|10.0.0.1||
|Servidor DNS preferencial|10.0.0.2||
|Servidor DNS alternativo|10.0.0.15||

- [Renomear o computador](#BKMK_rename)

|Item de configuração|Valor de exemplo|Valor|
|----------------------|-----------------|---------|
|Nome do computador|NPS1||

##### <a name="network-policy-server-installation-configuration-items"></a>Itens de configuração de instalação do Servidor de Políticas de Rede
Itens de configuração para os procedimentos de implantação NPS da rede do Windows Server Core [instalam o NPS (servidor de políticas de rede)](#BKMK_installNPS) e [registram o NPS no domínio padrão](#BKMK_registerNPS).

- Nenhum item de configuração adicional é necessário para instalar e registrar o NPS.
