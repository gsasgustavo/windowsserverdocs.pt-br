---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: Lista de verificação - como configurar um Proxy do servidor de Federação
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c8cd5cbe2ce0c7985a56f8444edfa7c71ee17c2d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192353"
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>Lista de verificação: Configurando um Proxy do Servidor de Federação

Esta lista de verificação inclui as tarefas de implantação para preparar um servidor que executa o Windows Server® 2012 para a função do proxy do servidor de federação nos serviços de Federação do Active Directory \(do AD FS\).  
  
> [!NOTE]  
> Execute as tarefas desta lista de verificação na ordem indicada. Quando um link de referência levar você a um procedimento, volte para este tópico depois de executar as etapas nesse procedimento para que você possa prosseguir com as tarefas restantes na lista de verificação.  
  
![Configurando um servidor proxy federado](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**lista de verificação: Como configurar um proxy do servidor de Federação**  
  
||Tarefa|Referência|  
|-|--------|-------------|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Antes de você começar a implantar os proxies de servidor de Federação do AD FS, examine os tipos de topologia de implantação do AD FS e seu posicionamento do servidor associado e recomendações de layout de rede.|![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[determinar a topologia de implantação do AD FS](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[planejamento colocação de Proxy de servidor de Federação](https://technet.microsoft.com/library/dd807130.aspx)<br /><br />![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[onde colocar um Proxy do servidor de Federação](https://technet.microsoft.com/library/dd807048.aspx)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Examine a capacidade do AD FS, orientação de planejamento para determinar o número adequado de proxies de servidor de federação, que você deve usar em seu ambiente de produção.|![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[planejamento de capacidade do Proxy de servidor de Federação](https://technet.microsoft.com/library/gg749898.aspx)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Determine se um proxy do servidor de Federação único ou um farm de proxy do servidor de Federação é melhor para sua implantação. **Observação:** Servidores de Federação também executam as responsabilidades de proxy de servidor de Federação.|![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[quando criar um Proxy do servidor de Federação](https://technet.microsoft.com/library/dd807032.aspx)<br /><br />![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[quando criar um Farm de Proxy do servidor de Federação](https://technet.microsoft.com/library/dd807082.aspx)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Determine se esse novo proxy de servidor de Federação será criada na rede de perímetro da organização do parceiro de conta ou a organização do parceiro de recurso.|![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[revisar a função de Proxy do servidor de federação no parceiro de conta](https://technet.microsoft.com/library/dd807109.aspx)<br /><br />![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[revisar a função de Proxy do servidor de federação no parceiro de recurso](https://technet.microsoft.com/library/dd807052.aspx)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Antes de instalar o AD FS em um computador que se tornará um proxy do servidor de federação, leia sobre a importância de se obter um servidor de certificado de autenticação — para farms de proxy do servidor de Federação — adicionando ou compartilhamento de certificados em todos os servidores em um farm.|![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[requisitos de certificado para Proxies de servidor de Federação](https://technet.microsoft.com/library/dd807054.aspx)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Revise as informações no guia de Design do AD FS sobre como atualizar o sistema de nomes de domínio \(DNS\) na rede de perímetro, portanto, essa resolução de nome bem-sucedida para servidores de Federação e proxies de servidor de Federação pode ocorrer.|![Configurando um servidor proxy federado](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Name Resolution Requirements for Federation Server Proxies](https://technet.microsoft.com/library/dd807055.aspx)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Determine se o proxy do servidor de federação deve ser associado a um domínio. Embora os proxies de servidor de Federação não precisa ser associado a um domínio, eles são mais fáceis de gerenciar com recursos de diretiva de grupo e a administração remota quando eles são adicionados a um domínio.|![Configurando um servidor proxy federado](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ingressar um computador em um domínio](Join-a-Computer-to-a-Domain.md)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Dependendo de como a infraestrutura DNS na rede de perímetro é configurada, conclua um dos procedimentos nos tópicos à direita antes de implantar um proxy do servidor de federação na sua organização. **Observação:** Não execute dois procedimentos. Leia [Name Resolution Requirements for Federation Server Proxies](https://technet.microsoft.com/library/dd807055.aspx) para determinar qual procedimento que melhor atenda os requisitos da sua organização.|![Configurando um servidor proxy federado](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[configurar a resolução de nomes para um Proxy do servidor de Federação em uma zona DNS que atende apenas a rede de perímetro](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<br /><br />![Configurando um servidor proxy federado](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[configurar a resolução de nomes para um Proxy do servidor de Federação em um DNS zona que serve tanto a rede de perímetro e os clientes da Internet](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Depois de obter um servidor de certificado de autenticação, você deve instalá-lo nos serviços de informações da Internet \(IIS\) no site da Web padrão do proxy de servidor de Federação.|![Configurando um servidor proxy federado](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[importar um certificado de autenticação de servidor para o Site padrão](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|\(Opcional\) como uma alternativa para a obtenção de um servidor de certificado de autenticação de uma autoridade de certificação \(autoridade de certificação\), você pode usar o IIS para adquirir um certificado de exemplo para o proxy de servidor de Federação.<br /><br />Como o IIS gera um self\-certificado assinado que não se originam de uma fonte confiável, usá-lo para criar um\-assinou o certificado apenas nos seguintes cenários:<br /><br />-Quando você precisa criar um Secure Sockets Layer \(SSL\) canal entre o servidor e um grupo limitado, conhecido de usuários<br />-Quando você tem que solucionar problemas de terceiro\-problemas de certificado de terceiros **cuidado:** Não é uma prática recomendada de segurança para implantar um proxy do servidor de Federação em um ambiente de produção usando um self\-assinado, certificado de autenticação de servidor.|![Configurando um servidor proxy federado](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: Criar um\-assinou o certificado do servidor](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Instale o serviço de função Proxy do serviço de federação no computador que se tornará o proxy do servidor de Federação.|![Configurando um servidor proxy federado](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[instalar o serviço de função Proxy de serviço de Federação](Install-the-Federation-Service-Proxy-Role-Service.md)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Configure o software AD FS no computador para atuar na função proxy do servidor de Federação usando o Assistente de configuração de Proxy de servidor AD FSFederation.|![Configurando um servidor proxy federado](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[configurar um computador para a função de Proxy do servidor de Federação](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)|  
|![como configurar um servidor proxy federado](media/icon_checkboxo.gif)|Usando o Visualizador de Eventos, verifique se o serviço proxy de servidor de federação foi iniciado.|![Configurando um servidor proxy federado](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Verifique um Federation Server Proxy está operacional](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|  