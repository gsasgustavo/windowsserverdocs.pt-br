---
title: Desempenho e produtividade de túnel GRE de Gateway RAS
description: Este tópico, destinado a profissionais de ti (tecnologia da informação), fornece informações de desempenho de taxa de transferência sobre túneis de túnel de roteamento genérico (GRE) do gateway RAS.
manager: brianlic
ms.topic: article
ms.assetid: c051b2ec-de0f-49d1-82b9-5742b259cd7c
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: fceb3ff5421be65a9bb25ae74510257f70d0aaa6
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946772"
---
# <a name="ras-gateway-gre-tunnel-throughput-and-performance"></a>Desempenho e produtividade de túnel GRE de Gateway RAS

>Aplica-se a: \( canal semestral do Windows Server\)

Você pode usar este tópico para saber mais sobre o \( \) desempenho de túnel de protocolo GRE do gateway RAS do servidor de acesso remoto \( \) no Windows Server, versão 1709, em um \( ambiente de \) teste baseado em sistema de rede definido por Sdn sem software.

O gateway de RAS é um roteador de software e gateway que você pode usar no modo de locatário único ou em modo multilocatário. Este tópico discute um modo de locatário único, configuração de alta disponibilidade com clustering de failover. As estatísticas de desempenho do túnel GRE apresentadas neste tópico são válidas para o gateway RAS nos modos locatário Singele e multilocatário.

>[!NOTE]
>O clustering de failover é um recurso do Windows Server que permite agrupar vários servidores juntos em um cluster tolerante a falhas. Para obter mais informações, consulte [clustering de failover](../../../failover-clustering/failover-clustering-overview.md)

O modo de locatário único permite que organizações de qualquer tamanho implantem o gateway como um servidor de VPN de rede virtual privada de borda da Internet ou de \- perímetro \( \) . No modo de locatário único, você pode implantar o gateway RAS em um servidor físico ou VM de máquina virtual \( \) . Este tópico descreve a implantação de gateway de RAS em duas VMs de máquinas virtuais \( \) configuradas em um cluster de failover.

>[!IMPORTANT]
>Como os túneis GRE fornecem encapsulamento, mas não criptografia, você não deve usar o gateway de RAS configurado com o GRE como um gateway de borda da Internet. Para saber mais sobre os melhores usos do gateway RAS com túneis GRE, consulte [túnel GRE no Windows Server](gre-tunneling-windows-server.md).

O GRE é um protocolo de encapsulamento leve que pode encapsular uma ampla variedade de protocolos de camada de rede dentro de links de ponto virtual \- para \- ponto por meio de uma interconexão de Internet de protocolo IP. A implementação do Microsoft GRE encapsula tanto o IPv4 quanto o IPv6.

Para obter mais informações, consulte a seção **cenários de implantação de gateway de Ras** no tópico gateway de [RAS](./ras-gateway.md#bkmk_deploy).

Neste cenário de teste, que é descrito na ilustração a seguir, o fluxo de tráfego medido é movido da intranet da organização 2 para a intranet da organização 1. As VMs de carga de trabalho do locatário enviam o tráfego de rede da intranet 2 para a intranet 1 usando o gateway RAS.

![Visão geral do cenário de teste do túnel GRE do gateway de RAS](../../media/GRE-Tunnel-Perf/Gre-Infrastructure.jpg)

## <a name="test-environment-configuration"></a>Configuração do ambiente de teste

Esta seção fornece informações sobre o ambiente de teste e a configuração de gateway de RAS.

No ambiente de teste, as VMs de gateway de RAS são implantadas em \- hosts Hyper V em um cluster de failover para alta disponibilidade.

### <a name="hyper-v-host-configuration"></a>Configuração de host do Hyper- \- V

Dois \- hosts Hyper-V são configurados para dar suporte ao cenário de teste da seguinte maneira.

- Dois \- computadores físicos de hospedagem dupla são configurados com o Windows Server, versão 1709
- Os dois adaptadores de rede física em cada um dos dois servidores estão conectados a sub-redes diferentes – ambos representam sub-redes de uma intranet da organização. As redes e o hardware de suporte têm uma capacidade de 10 GBps.
- O hyperthreading nos servidores físicos está desabilitado. Isso fornece a taxa de transferência máxima das NICs físicas.
- A \- função de servidor Hyper v é instalada em ambos os servidores e configurada com dois \- comutadores virtuais Hyper-v externos, um para cada adaptador de rede física.
- Como ambos os servidores estão conectados à mesma intranet, os servidores podem se comunicar entre si.
- Os \- hosts do Hyper V são configurados em um cluster de failover pela rede da intranet.

>[!NOTE]
>Para saber mais, consulte [Comutador Virtual do Hyper-V](../../../virtualization/hyper-v-virtual-switch/hyper-v-virtual-switch.md).

### <a name="vm-configuration"></a>Configuração da VM

Duas VMs são configuradas para dar suporte ao cenário de teste da seguinte maneira.

- Em cada servidor, uma VM é instalada que está executando o Windows Server, versão 1709. Cada VM é configurada com 10 núcleos e 8 GB de RAM.
- Cada VM também é configurada com dois adaptadores de rede virtual. Um adaptador de rede virtual está conectado ao comutador virtual da intranet 1 e o outro adaptador de rede virtual está conectado ao comutador virtual da intranet 2.
- Cada VM tem um gateway de RAS instalado e configurado como um \- servidor VPN baseado em GRE.
- As VMs de gateway são configuradas em um cluster de failover. Quando clusterizado, uma VM está ativa e a outra VM é passiva.

### <a name="workload-hyper-v-hosts-and-vms"></a>\-VMs e hosts Hyper V de carga de trabalho

Para esse teste, dois hosts Hyper V de carga de trabalho \- são instalados na intranet e cada host tem uma VM instalada. Se você estiver duplicando esse teste em seu próprio ambiente de teste, poderá instalar quantos servidores de carga de trabalho e VMs forem apropriados para suas finalidades.

- \-Os hosts Hyper V de carga de trabalho têm um adaptador de rede física instalado que está conectado à intranet da organização.
- No \- comutador virtual do Hyper-V, um comutador virtual é criado em cada host. A opção é externa e está associada a um adaptador de rede conectado à intranet.
- As VMs de carga de trabalho são configuradas com 2 GB de RAM e 2 núcleos.
- As VMs de carga de trabalho têm um adaptador de rede virtual que está conectado ao comutador virtual de intranet.

### <a name="traffic-generator-tool"></a>Ferramenta de gerador de tráfego

A ferramenta de gerador de tráfego usada neste teste é a ferramenta ctsTraffic. O repositório Git para essa ferramenta está localizado em [https://github.com/Microsoft/ctsTraffic](https://github.com/Microsoft/ctsTraffic) .

## <a name="ras-gateway-performance"></a>Desempenho do gateway RAS

As ilustrações nesta seção descrevem as exibições do Gerenciador de tarefas da taxa de transferência do túnel GRE com várias conexões TCP.

Você pode alcançar uma taxa de transferência de até 2,0 Gbps em VMs de vários \- núcleos configuradas como gateways de RAS do GRE.

### <a name="gre-tunnel-performance-with-multiple-tcp-sessions"></a>Desempenho do túnel GRE com várias sessões TCP

Com várias sessões TCP, a utilização da CPU atinge 100% e a taxa de transferência máxima no túnel GRE é de 2,0 Gbps.

A ilustração a seguir descreve a utilização da CPU em ambas as VMs de gateway de RAS. A VM ativa, a VM do gateway RAS #1, está à esquerda, enquanto a VM passiva, a VM do gateway RAS #2, está à direita.

![Utilização da CPU da VM do gateway no Gerenciador de tarefas](../../media/GRE-Tunnel-Perf/Gre-Tunnel-01.jpg)

A ilustração a seguir ilustra a taxa de transferência da rede Ethernet nas VMs do gateway de RAS. A VM ativa, a VM do gateway RAS #1, está à esquerda, enquanto a VM passiva, a VM do gateway RAS #2, está à direita.

![Taxa de transferência de rede Ethernet de VM de gateway no Gerenciador de tarefas](../../media/GRE-Tunnel-Perf/Gre-Tunnel-02.jpg)


### <a name="gre-tunnel-performance-with-one-tcp-connection"></a>Desempenho do túnel GRE com uma conexão TCP

Com a configuração de teste alterada de várias sessões TCP para uma única sessão TCP, apenas um núcleo de CPU atinge a capacidade máxima nas VMs do gateway de RAS.

A taxa de transferência máxima no túnel GRE está entre 400-500 Mbps.

A ilustração a seguir descreve a utilização da CPU em ambas as VMs de gateway de RAS. A VM ativa, a VM do gateway RAS #1, está à esquerda, enquanto a VM passiva, a VM do gateway RAS #2, está à direita.

![Utilização da CPU da VM do gateway no Gerenciador de tarefas](../../media/GRE-Tunnel-Perf/Gre-Tunnel-03.jpg)


A ilustração a seguir ilustra a taxa de transferência da rede Ethernet nas VMs do gateway de RAS. A VM ativa, a VM do gateway RAS #1, está à esquerda, enquanto a VM passiva, a VM do gateway RAS #2, está à direita.

![Taxa de transferência de rede Ethernet de VM de gateway no Gerenciador de tarefas](../../media/GRE-Tunnel-Perf/Gre-Tunnel-04.jpg)

Para obter mais informações sobre o desempenho do gateway RAS, consulte [ajuste de desempenho do gateway HNV em redes definidas pelo software](../../../administration/performance-tuning/subsystem/software-defined-networking/hnv-gateway-performance.md).
