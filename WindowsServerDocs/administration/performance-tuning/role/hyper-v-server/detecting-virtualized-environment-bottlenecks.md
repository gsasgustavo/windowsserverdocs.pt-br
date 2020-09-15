---
title: Detectar gargalos em um ambiente virtualizado
description: Como detectar e resolver possíveis afunilamentos de desempenho do Hyper-v
ms.topic: article
ms.author: asmahi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: cc072d51623d53539bcf27dfaf950e4ba1621e71
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077243"
---
# <a name="detecting-bottlenecks-in-a-virtualized-environment"></a>Detectar gargalos em um ambiente virtualizado

Esta seção deve fornecer algumas dicas sobre o que monitorar usando o monitor de desempenho e como identificar onde o problema pode ocorrer quando o host ou algumas das máquinas virtuais não são executadas como você esperava.

## <a name="processor-bottlenecks"></a>Afunilamentos de processador

Aqui estão alguns cenários comuns que poderiam causar afunilamentos de processador:

-   Um ou mais processadores lógicos estão carregados

-   Um ou mais processadores virtuais estão carregados

Você pode usar os seguintes contadores de desempenho do host:

-   Utilização do processador lógico- \\ processador lógico do hipervisor Hyper-V ( \* ) \\ % tempo de execução total

-   Utilização do processador virtual- \\ processador virtual do hipervisor Hyper-V ( \* ) \\ % tempo de execução total

-   Utilização do processador virtual raiz- \\ processador virtual raiz do hipervisor Hyper-V ( \* ) \\ % tempo de execução total

Se o contador do **processador lógico do hipervisor do Hyper-V ( \_ total) \\ % total de tempo de execução** estiver acima de 90%, o host estará sobrecarregado. Você deve adicionar mais capacidade de processamento ou mover algumas máquinas virtuais para um host diferente.

Se o contador **virtual do hipervisor do Hyper-V (nome da VM: VP x) \\ % tempo de execução total** for superior a 90% para todos os processadores virtuais, você deverá fazer o seguinte:

-   Verifique se o host não está sobrecarregado

-   Descubra se a carga de trabalho pode aproveitar mais processadores virtuais

-   Atribuir mais processadores virtuais à máquina virtual

Se o **processador virtual do hipervisor Hyper-V (nome da VM: VP x) \\ % total** do contador de tempo de execução for de mais de 90% para alguns, mas não todos, dos processadores virtuais, você deverá fazer o seguinte:

-   Se sua carga de trabalho receber uso intensivo de rede, você deverá considerar o uso de vRSS.

-   Se as máquinas virtuais não estiverem executando o Windows Server 2012 R2, você deverá adicionar mais adaptadores de rede.

-   Se sua carga de trabalho for de uso intensivo de armazenamento, você deverá habilitar o NUMA virtual e adicionar mais discos virtuais.

Se o contador de **tempo de execução do processador virtual do hipervisor do Hyper-V (VP raiz x) \\ % total de Runtime** for de mais de 90% para alguns, mas nem todos os processadores virtuais e o contador **processador (x) \\ % tempo de interrupção e processador (x) \\ % tempo de DPC** aproximadamente aumentam para o valor do contador do **processador virtual raiz (VP raiz x) \\ % total** de tempo de execução, você deve garantir a habilitação da VMQ nos adaptadores de rede.

## <a name="memory-bottlenecks"></a>Gargalos de memória

Aqui estão alguns cenários comuns que podem causar gargalos de memória:

-   O host não está respondendo.

-   As máquinas virtuais não podem ser iniciadas.

-   As máquinas virtuais ficam sem memória.

Você pode usar os seguintes contadores de desempenho do host:

-   MB de memória \\ disponível

-   Memória disponível do balanceador de Memória Dinâmica do Hyper-V ( \* ) \\

Você pode usar os seguintes contadores de desempenho da máquina virtual:

-   MB de memória \\ disponível

Se os contadores de memória ** \\ disponíveis de Mbytes** e de **memória dinâmica do Hyper-V ( \* ) \\ disponíveis** estiverem insuficientes no host, você deverá parar os serviços não essenciais e migrar uma ou mais máquinas virtuais para outro host.

Se o contador **memória \\ disponível em Mbytes** estiver baixo na máquina virtual, você deverá atribuir mais memória à máquina virtual. Se você estiver usando Memória Dinâmica, deverá aumentar a configuração de memória máxima.

## <a name="network-bottlenecks"></a>Afunilamentos de rede

Aqui estão alguns cenários comuns que poderiam causar afunilamentos de rede:

-   O host está associado à rede.

-   A máquina virtual está ligada à rede.

Você pode usar os seguintes contadores de desempenho do host:

-   Interface de rede (*nome do adaptador de rede*) \\ bytes/s

Você pode usar os seguintes contadores de desempenho da máquina virtual:

-   Adaptador de rede virtual do Hyper-V (* &lt; GUID &gt; de nome de máquina virtual*) \\ bytes/s

Se o contador **bytes de NIC física/s** for maior ou igual a 90% da capacidade, você deverá adicionar adaptadores de rede adicionais, migrar máquinas virtuais para outro host e configurar a QoS de rede.

Se o contador **bytes/s do adaptador de rede virtual do Hyper-V** for maior ou igual a 250 Mbps, você deverá adicionar adaptadores de rede agrupados adicionais na máquina virtual, habilitar o vRSS e usar o Sr-iov.

Se suas cargas de trabalho não puderem atender à latência de rede, habilite a SR-IOV para apresentar os recursos do adaptador de rede física à máquina virtual.

## <a name="storage-bottlenecks"></a>Afunilamentos de armazenamento

Aqui estão alguns cenários comuns que poderiam causar gargalos de armazenamento:

-   As operações de host e máquina virtual são lentas ou expiram.

-   A máquina virtual está lenta.

Você pode usar os seguintes contadores de desempenho do host:

-   Disco físico (*letra do disco*) \\ média de disco s/leitura

-   Disco físico (*letra do disco*) \\ média de disco s/gravação

-   Disco físico (*letra do disco*) \\ comprimento médio da fila de leitura de disco

-   Disco físico (*letra do disco*) \\ comprimento médio da fila de gravação de disco

Se as latências forem consistentemente maiores que 50 ms, você deverá fazer o seguinte:

-   Distribuir máquinas virtuais entre armazenamentos adicionais

-   Considere comprar um armazenamento mais rápido

-   Considere os espaços de armazenamento em camadas, que foram introduzidos no Windows Server 2012 R2

-   Considere o uso de QoS de armazenamento, que foi introduzido no Windows Server 2012 R2

-   Usar VHDX

## <a name="additional-references"></a>Referências adicionais

-   [Terminologia do Hyper-V](terminology.md)

-   [Arquitetura Hyper-V](architecture.md)

-   [Configuração do servidor do Hyper-V](configuration.md)

-   [Desempenho do processador do Hyper-V](processor-performance.md)

-   [Desempenho de memória do Hyper-V](memory-performance.md)

-   [Desempenho de E/S de armazenamento do Hyper-V](storage-io-performance.md)

-   [Desempenho de E/S de rede do Hyper-V](network-io-performance.md)

-   [Máquinas virtuais do Linux](linux-virtual-machine-considerations.md)
