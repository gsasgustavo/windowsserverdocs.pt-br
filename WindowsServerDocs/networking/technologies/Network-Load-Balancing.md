---
title: Network Load Balancing
description: Neste tópico, fornecemos uma visão geral do recurso NLB de balanceamento de carga de rede \( \) no Windows Server 2016. Você pode usar o NLB para gerenciar dois ou mais servidores como um único cluster virtual. O NLB aprimora a disponibilidade e a escalabilidade de aplicativos de servidor de Internet, como aqueles usados em Web, FTP, firewall, proxy, VPN de rede privada virtual \( \) e outros servidores de missão \- crítica.
manager: dougkim
ms.topic: article
ms.assetid: 244a4b48-06e5-4796-8750-a50e4f88ac72
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: 2edcd046958854698fbcc61d96f2716a26de3367
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96866265"
---
# <a name="network-load-balancing"></a>Network Load Balancing

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Neste tópico, fornecemos uma visão geral do recurso NLB de balanceamento de carga de rede \( \) no Windows Server 2016. Você pode usar o NLB para gerenciar dois ou mais servidores como um único cluster virtual. O NLB aprimora a disponibilidade e a escalabilidade de aplicativos de servidor de Internet, como aqueles usados em Web, FTP, firewall, proxy, VPN de rede privada virtual \( \) e outros servidores de missão \- crítica.

> [!NOTE]
> O Windows Server 2016 inclui um novo software inspirado pelo Azure Load Balancer \( SLB \) como um componente da infraestrutura de Sdn de rede definida pelo software \( \) . Use SLB em vez de NLB se você estiver usando o SDN, usando cargas de trabalho não Windows, precisar de NAT de conversão de endereços de rede \( \) de saída ou necessidade de balanceamento de carga de camada 3 \( L3 \) ou não baseado em TCP. Você pode continuar a usar o NLB com o Windows Server 2016 para implantações não SDN. Para obter mais informações sobre SLB, consulte [balanceamento de carga de software (SLB) para Sdn](../sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md).

O recurso NLB de balanceamento de carga de rede \( \) distribui o tráfego entre vários servidores usando o \/ protocolo de rede IP TCP. Ao combinar dois ou mais computadores que estão executando aplicativos em um único cluster virtual, o NLB fornece confiabilidade e desempenho para servidores Web e outros \- servidores de missão crítica.

Os servidores em um cluster NLB se chamam *hosts*, e cada host executa uma cópia separada dos aplicativos de servidor. O NLB distribui as solicitações de entrada dos clientes pelos hosts do cluster. É possível configurar a carga que será tratada por cada host. Você também pode adicionar hosts dinamicamente ao cluster para tratar aumentos de carga. Além disso, o NLB pode direcionar todo o tráfego para um único host designado, chamado de *host padrão*.

O NLB permite que todos os computadores no cluster sejam abordados pelo mesmo conjunto de endereços IP, e mantém um conjunto de endereços IP exclusivos e dedicados para cada host. Para aplicativos com balanceamento de carga \- , quando um host falha ou fica offline, a carga é redistribuída automaticamente entre os computadores que ainda estão operando. Quando estiver pronto, o computador offline poderá reintegrar-se ao cluster de forma transparente e retomar sua parcela da carga de trabalho, o que permite que os outros computadores do cluster lidem com menos tráfego.

## <a name="practical-applications"></a>Aplicações práticas
O NLB é útil para garantir que aplicativos sem estado, como servidores Web que executam Serviços de Informações da Internet \( IIS \) , estejam disponíveis com tempo de inatividade mínimo e que sejam escalonáveis \( adicionando mais servidores à medida que a carga aumenta \) . As seções a seguir descrevem como o NLB suporta alta disponibilidade, escalabilidade e gerenciamento dos servidores em cluster que executam esses aplicativos.

### <a name="high-availability"></a>Alta disponibilidade
Um sistema altamente disponível oferece, de forma confiável, um nível aceitável de serviço com tempo de inatividade mínimo. Para fornecer alta disponibilidade, o NLB inclui \- recursos internos que podem automaticamente:

-   Detectar um host de cluster que falha ou fica offline, e depois recuperar.

-   Equilibrar a carga da rede quando hosts são adicionados ou removidos.

-   Recuperar e redistribuir carga de trabalho no prazo de dez segundos.

### <a name="scalability"></a>Escalabilidade
Escalabilidade é a medida que determina como um computador, serviço ou aplicativo pode atender melhor às necessidades crescentes de desempenho. No caso de clusters NLB , a escalabilidade é a capacidade de adicionar paulatinamente um ou mais sistemas a um cluster existente quando a carga total sobre o cluster excede seus recursos. Para dar suporte à escalabilidade, o NLB pode fazer o seguinte:

-   Equilibre solicitações de carga no cluster NLB para serviços IP individuais de TCP \/ .

-   Dar suporte para até 32 computadores em um único cluster.

-   Equilibre várias solicitações \( de carga de servidor do mesmo cliente ou de vários clientes em \) vários hosts no cluster.

-   Adicionar hosts ao cluster do NLB à medida que a carga aumenta, sem fazer o cluster falhar.

-   Remover os hosts do cluster quando a carga diminui.

-   Permitir alto desempenho e baixa sobrecarga através de implementação com pipelining integral. O pipelining permite que as solicitações sejam enviadas ao cluster NLB sem aguardar resposta da solicitação enviada anteriormente.

### <a name="manageability"></a>Capacidade de gerenciamento
Para dar suporte à escalabilidade, o NLB pode fazer o seguinte:

-   Gerencie e configure vários clusters NLB e os hosts de cluster de um único computador usando o Gerenciador NLB ou os [cmdlets NLB (balanceamento de carga de rede) no Windows PowerShell](/previous-versions/windows/powershell-scripting/hh801274(v=wps.630)).

-   Especificar o comportamento do balanceamento de carga para uma única porta ou para um grupo de portas IP usando regras de gerenciamento de portas.

-   Definir regras de porta diferentes para cada site. Se você usar o mesmo conjunto de \- servidores com balanceamento de carga para vários aplicativos ou sites, as regras de porta serão baseadas no endereço IP virtual de destino \( usando clusters virtuais \) .

-   Encaminhe todas as solicitações de cliente para um único host usando regras de host único opcionais \- . O NLB roteia solicitações de clientes para um host específico que esteja executando aplicativos específicos.

-   Bloquear o acesso indesejado à rede para determinadas portas IP.

-   Habilite o suporte IGMP do protocolo de gerenciamento de grupo da Internet \( \) nos hosts do cluster para controlar a saturação da porta do comutador \( em que os pacotes de rede de entrada são enviados para todas as portas no comutador \) ao operar no modo multicast.

-   Iniciar, parar e controlar as ações NLB remotamente usando comandos do Windows PowerShell ou scripts.

-   Exibir o log de eventos do Windows para verificar eventos do NLB. O NLB registra todas as ações e alterações de cluster no log de eventos.

## <a name="important-functionality"></a>Funcionalidade importante

O NLB é instalado como um componente padrão de driver de rede do Windows Server. Suas operações são transparentes para a \/ pilha de rede IP TCP. A figura a seguir mostra a relação entre o NLB e outros componentes de software em uma configuração típica.

![Balanceamento de carga de rede e outros componentes de software](../media/NLB/nlb.jpg)

A seguir estão os principais recursos do NLB.

- Não requer alterações de hardware para funcionar.

- Oferece Ferramentas de Balanceamento de Carga de Rede para configurar e gerenciar vários clusters e todos os hosts do cluster em um único computador remoto ou local.

- Permite que os clientes acessem o cluster usando um único nome de Internet lógico e um endereço IP virtual, que é conhecido como o endereço IP do cluster, \( ele retém os nomes individuais de cada computador \) . O NLB permite vários endereços IP virtuais para servidores multihomed.

> [!NOTE]
> Quando você implanta VMs como clusters virtuais, o NLB não exige que os servidores sejam de hospedagem múltipla para ter vários endereços IP virtuais.

- Permite que o NLB seja vinculado a vários adaptadores de rede, o que permite configurar vários clusters independentes em cada host. O suporte a vários adaptadores de rede difere dos clusters virtuais, pois os clusters virtuais permitem configurar vários clusters em um único adaptador de rede.

- Não requer modificações de aplicativos de servidor para que eles possam ser executados em um cluster NLB.

- Pode ser configurado para adicionar automaticamente um host ao cluster se esse host de cluster falhar e voltar ao modo online posteriormente. O host adicionado pode começar a manipular os pedidos de novos servidores clientes.

-   Permite que você coloque computadores offline para manutenção preventiva sem perturbar as operações de cluster nos outros hosts.

## <a name="hardware-requirements"></a>Requisitos de hardware
A seguir estão os requisitos de hardware para executar um cluster NLB.

-   Todos os hosts do cluster devem residir na mesma sub-rede.

-   Não há restrição ao número de adaptadores de rede em cada host, e hosts diferentes podem ter um número diferente de adaptadores.

-   Dentro de cada cluster, todos os adaptadores de rede devem ser multicast ou unicast. O NLB não dá suporte a ambientes mistos unicast e multicast em um único cluster.

-   Se você usar o modo unicast, o adaptador de rede que é usado para \- manipular \- o cliente para o tráfego de cluster deve dar suporte à alteração do seu endereço MAC de controle de acesso à mídia \( \) .

## <a name="software-requirements"></a>Requisitos de software
A seguir estão os requisitos de software para executar um cluster NLB.

-   Somente TCP \/ IP pode ser usado no adaptador para o qual o NLB está habilitado em cada host. Não adicione nenhum outro protocolo \( , por exemplo, IPX \) a esse adaptador.

-   Os endereços IP dos servidores no cluster devem ser estáticos.

> [!NOTE]
> O NLB não dá suporte ao DHCP do protocolo de configuração de host dinâmico \( \) . O NLB desabilita o DHCP em cada interface que ele configura.

## <a name="installation-information"></a>Informações de instalação
Você pode instalar o NLB usando o Gerenciador do Servidor ou os comandos do Windows PowerShell para NLB.

Opcionalmente, você pode instalar as Ferramentas de Balanceamento de Carga de Rede para gerenciar um cluster NLB local ou remoto. As ferramentas incluem o Gerenciador de balanceamento de carga de rede e os comandos NLB do Windows PowerShell.

### <a name="installation-with-server-manager"></a>Instalação com o Gerenciador do Servidor

No Gerenciador do Servidor, você pode usar o assistente para adicionar funções e recursos para adicionar o recurso de **balanceamento de carga de rede** . Quando você concluir o assistente, o NLB será instalado e não será necessário reiniciar o computador.


### <a name="installation-with-windows-powershell"></a>Instalação com o Windows PowerShell

Para instalar o NLB usando o Windows PowerShell, execute o seguinte comando em um prompt elevado do Windows PowerShell no computador em que você deseja instalar o NLB.

```powershell
Install-WindowsFeature NLB -IncludeManagementTools
```

Após a conclusão da instalação, não é necessário reiniciar o computador.

Para obter mais informações, consulte [Install-WindowsFeature](/powershell/module/servermanager/install-windowsfeature).

### <a name="network-load-balancing-manager"></a>Gerenciador de balanceamento de carga de rede
Para abrir o Gerenciador de Balanceamento de Carga de Rede em um Gerenciador do Servidor, clique em **Ferramentas** e depois clique em **Gerenciador de Balanceamento de Carga de Rede**.

## <a name="additional-resources"></a>Recursos adicionais
A tabela a seguir fornece links para informações adicionais sobre o recurso NLB.

|Tipo de conteúdo|Referências|
|----------------|--------------|
|Implantação|[Guia de implantação de balanceamento de carga de rede](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754833(v=ws.10)) &#124; configurar o [balanceamento de carga de rede com serviços de terminal](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771300(v=ws.10))|
|Operations|[Gerenciar clusters de balanceamento de carga de rede](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753954(v=ws.10)) &#124; [definir parâmetros de balanceamento de carga de rede](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731619(v=ws.10)) &#124; [controlar hosts em clusters de balanceamento de carga de rede](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770870(v=ws.10))|
|Solução de problemas|[Solucionando problemas de clusters de balanceamento de carga de rede](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732592(v=ws.10)) &#124; [eventos e erros de cluster NLB](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731678(v=ws.10))|
|Ferramentas e configurações|[Cmdlets do Windows PowerShell para Balanceamento de Carga de Rede](https://go.microsoft.com/fwlink/p/?LinkId=238123)|
|Recursos da comunidade|[Fórum de \( clustering de alta disponibilidade \)](https://go.microsoft.com/fwlink/p/?LinkId=230641)
