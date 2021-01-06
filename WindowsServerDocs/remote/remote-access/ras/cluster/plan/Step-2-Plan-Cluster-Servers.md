---
title: Etapa 2 planejar servidores de cluster
description: Este tópico faz parte do guia implantar o acesso remoto em um cluster no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 673c5bfb-b590-4932-8e54-ca0a466d90cc
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: cca4e4483875b5a9e8eaebc2b5983087ee8fbbc6
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947752"
---
# <a name="step-2-plan-cluster-servers"></a>Etapa 2 planejar servidores de cluster

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Depois de implantar um único servidor de acesso remoto, planeje adicionar servidores adicionais ao cluster.

|Tarefa|Descrição|
|----|--------|
|[2,1 Instalando funções e recursos](#BKMK_Install).|Para cada servidor que será adicionado ao cluster, planeje a instalação da função de acesso remoto e o recurso NLB do Windows (se necessário), planeje a topologia, o endereçamento IP, o roteamento e o encaminhamento.|
|[2,2 definir configurações do servidor](#BKMK_Config)|Defina as configurações para cada servidor que será adicionado ao cluster. Observe que você pode configurar um cluster com balanceamento de carga de servidores usando máquinas virtuais. Para que o roteamento e a conectividade funcionem corretamente, você deve configurar as máquinas virtuais para usar a falsificação de endereço MAC.|

## <a name="21-installing-roles-and-features"></a><a name="BKMK_Install"></a>2,1 Instalando funções e recursos
Para cada servidor que você deseja ingressar no cluster, planeje a instalação da função de acesso remoto. Além disso, planeje instalar o recurso NLB (balanceamento de carga de rede) se desejar balancear a carga do tráfego para o cluster usando o NLB do Windows. Para obter mais informações, consulte [balanceamento de carga de rede](../../../../../networking/technologies/network-load-balancing.md).

## <a name="22-configure-server-settings"></a><a name="BKMK_Config"></a>2,2 definir configurações do servidor
Para cada servidor que será adicionado ao cluster, planeje o endereço IP e as configurações de domínio. Observe o seguinte:

1.  Todos os servidores no cluster devem pertencer ao mesmo domínio.

2.  Os servidores no cluster devem estar localizados na mesma sub-rede.

3.  Cada servidor no cluster deve ter o mesmo número de adaptadores de rede em uso para a implantação do DirectAccess.

Ao balancear a carga do cluster usando o NLB do Windows, as seguintes configurações do NLB do Windows são aplicadas:

1.  Modo de operação-unicast. Isso pode ser alterado para multicast usando o Gerenciador NLB. Essa configuração não pode ser modificada no console de gerenciamento de acesso remoto.

2.  Fator de balanceamento de carga – definido como igual, em que todos os servidores de cluster têm carga igual.

3.  Modo de filtragem-o tráfego terá a carga balanceada entre vários hosts.

4.  Affinity-Single afinidade está definida.

5.  Protocols-Both
