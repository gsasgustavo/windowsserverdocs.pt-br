---
title: Gerenciar remotamente os clientes do DirectAccess
description: Este tópico faz parte do guia gerenciar clientes DirectAccess remotamente no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 36255d80-a13e-4af7-a5c0-ab4c8f302622
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 86824aaba3e249aa5cc4f0743d28ce0371481c21
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947732"
---
# <a name="manage-directaccess-clients-remotely"></a>Gerenciar remotamente os clientes do DirectAccess

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

O monitoramento de Acesso Remoto relata a atividade e o status do usuário remoto para o DirectAccess e as conexões VPN. Ele rastreia o número e a duração das conexões do cliente (entre outras estatísticas) e monitora o status das operações do servidor. Um console de monitoramento fácil de usar apresenta uma exibição de toda a infraestrutura de Acesso Remoto. As exibições de monitoramento estão disponíveis para configurações de servidor individual, cluster e multissite.

**Observação:** O Windows Server 2016 combina o DirectAccess e o serviço de acesso remoto (RAS) em uma única função de acesso remoto.

## <a name="in-this-guide"></a>Neste guia
Este documento contém instruções para você aproveitar os recursos de monitoramento do Acesso Remoto usando o console de gerenciamento do DirectAccess e os cmdlets correspondentes do Windows PowerShell, que são fornecidos como parte da função de servidor de Acesso Remoto.

Os seguintes cenários de monitoramento e contabilidade são explicados:

1.  Monitorar a carga existente no servidor de Acesso Remoto

2.  Monitorar o status de distribuição de configuração do servidor de Acesso Remoto

3.  Monitorar o status das operações do servidor de Acesso Remoto e seus componentes

4.  Identificar e resolver problemas de operações do servidor de Acesso Remoto

5.  Monitorar a atividade e o status de clientes remotos conectados

6.  Gerar um relatório de uso para clientes remotos utilizando dados históricos

### <a name="understand-monitoring-and-accounting"></a>Entender o monitoramento e contabilidade
Antes de iniciar as tarefas de monitoramento e contabilidade dos clientes remotos, você deve entender a diferença entre as duas.

-   **Monitoramento** mostra usuários ativamente conectados em determinado momento.

-   **Contabilidade** mantém um histórico dos usuários que se conectaram à rede corporativa e dos respectivos detalhes de uso (para fins de conformidade e auditoria).

O monitoramento de clientes remotos se baseia nas conexões. Existem dois tipos de conexões de túnel que são estabelecidas pelos clientes do DirectAccess:

-   **Conexões automáticas de tráfego de túnel**: esse túnel é estabelecido pelo computador, no contexto do sistema, a fim de acessar os servidores exigidos para a resolução de nomes, autenticação, atualização de correção e assim por diante.

-   **Conexões de tráfego de túnel do usuário**: esse túnel é estabelecido pela conta de usuário no computador, no contexto do usuário, quando este tenta acessar um recurso da rede corporativa. Dependendo dos requisitos de implantação, talvez o usuário precise fornecer credenciais fortes (por exemplo, usando um cartão inteligente ou especificando uma senha de uso único) para acessar os recursos da rede corporativa.

Para o DirectAccess, uma conexão é identificada exclusivamente pelo endereço IP do cliente remoto. Por exemplo, se o túnel de um computador estiver aberto para um computador cliente e um usuário estiver conectado a esse computador, eles usarão a mesma conexão. Em uma situação na qual o usuário se desconecta e conecta-se novamente enquanto o túnel do computador ainda está ativo, a conexão será individual.



