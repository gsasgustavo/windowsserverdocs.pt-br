---
title: Sintaxe e formatação do comando Pktmon
description: Use esta página para entender a sintaxe, os comandos, a formatação e a saída do pktmon para compilações do Windows vibranium.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 3e4c73af3b00f42301b34e59493f25b6d2ccb95c
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632389"
---
# <a name="pktmon-command-syntax-and-formatting"></a>Sintaxe e formatação do comando Pktmon

>Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

O monitor de pacotes (Pktmon) é uma ferramenta de diagnóstico de rede entre componentes para Windows. Ele pode ser usado para captura de pacotes, detecção de pacotes drop, filtragem de pacotes e contagem. A ferramenta é especialmente útil em cenários de virtualização, como rede de contêineres e SDN, pois fornece visibilidade dentro da pilha de rede. O monitor de pacotes está disponível na caixa por meio do comando pktmon.exe no sistema operacional vibranium (Build 19041). Você pode usar este tópico para aprender a entender a sintaxe do pktmon, a formatação de comandos e a saída.

## <a name="quick-start"></a>Início rápido

Use as seguintes etapas para começar em cenários genéricos:

1. Identifique o tipo de pacotes necessários para a captura, ou seja, endereços IP específicos, portas ou protocolos associados ao pacote. Em seguida, verifique a sintaxe para aplicar filtros de captura e aplique os filtros para os pacotes identificados na etapa anterior.

   ```PowerShell
   C:\Test> pktmon filter add help
   C:\Test> pktmon filter add <filters>
   ```

2. Inicie a captura e habilite o log de pacotes.

   ```PowerShell
   C:\Test> pktmon start --etw
   ```

3. Reproduzir o problema que está sendo diagnosticado. Consulte os contadores para confirmar a presença do tráfego esperado e para obter uma exibição de alto nível de como o tráfego fluiu no computador.

   ```PowerShell
   C:\Test> pktmon counters
   ```

4. Pare a captura e recupere os logs no formato txt para análise.

   ```PowerShell
   C:\Test> pktmon stop
   C:\Test> pktmon format <etl file>
   ```

Consulte [analisar saída do monitor de pacotes](#analyze-packet-monitor-output) para obter instruções sobre como analisar a saída txt.

## <a name="capture-filters"></a>Filtros de captura

É altamente recomendável aplicar filtros antes de iniciar qualquer captura de pacote, pois a solução de problemas de conectividade para um destino específico é mais fácil quando você se concentra em um único fluxo de pacotes. Capturar *todo* o tráfego de rede pode tornar a saída muito ruidosa para ser analisada. Para que um pacote seja relatado, ele deve corresponder a todas as condições especificadas em pelo menos um filtro. Há suporte para até 32 filtros ao mesmo tempo.

Por exemplo, o seguinte conjunto de filtros irá capturar qualquer tráfego ICMP de ou para o endereço IP 10.0.0.10, bem como qualquer tráfego na porta 53.

```PowerShell
C:\Test> pktmon filter add -i 10.0.0.10 -t icmp
C:\Test> pktmon filter add -p 53
```

### <a name="filtering-capability"></a>Capacidade de filtragem

- O monitor de pacotes dá suporte à filtragem por endereços MAC, endereços IP, portas, EtherType, protocolo de transporte e ID de VLAN. 

- O monitor de pacotes não fará distinção entre a origem ou o destino quando chegar ao endereço MAC, endereço IP ou filtros de porta. 

- Para filtrar ainda mais os pacotes TCP, é possível fornecer uma lista opcional de sinalizadores TCP para correspondência. Os sinalizadores com suporte são FIN, SYN, RST, PSH, ACK, URG, ECE e CWR.

  - Por exemplo, o filtro a seguir irá capturar todos os pacotes SYN enviados ou recebidos pelo endereço IP 10.0.0.10:

```PowerShell
C:\Test> pktmon filter add -i 10.0.0.10 -t tcp syn
```

- O monitor de pacotes pode aplicar um filtro a pacotes internos encapsulados, além do pacote externo, se o sinalizador [-e] foi adicionado a qualquer filtro. Os métodos de encapsulamento com suporte são VXLAN, GRE, NVGRE e IP-in-IP. A porta VXLAN personalizada é opcional e o padrão é 4789.

### <a name="pktmon-filters-syntax"></a>Sintaxe de filtros Pktmon

```PowerShell
C:\Test> pktmon filter help
pktmon filter { list | add | remove } [OPTIONS | help]

Commands
    list      Display active packet filters.
    add       Add a filter to control which packets are reported.
    remove    Removes all filters.

help
    Show help text for a command.

C:\Test> pktmon filter add help
pktmon filter add <name> [-m mac [mac2]] [-v vlan] [-d { IPv4 | IPv6 | number }]
                         [-t { TCP [flags...] | UDP | ICMP | ICMPv6 | number }]
                         [-i ip [ip2]] [-p port [port2]] [-e [port]]
    Add a filter to control which packets are reported. For a packet to be
    reported, it must match all conditions specified in at least one filter.
    Up to 8 filters can be active at once.

    NOTE1: When two MACs (-m), IPs (-i), or ports (-p) are specified, the filter
           matches packets that contain both. It will not distinguish between source
           or destination for this purpose.

name
    Optional name or description of the filter.

Ethernet frame
    -m, --mac[-address]
        Match source or destination MAC address. See NOTE1 above.

    -v, --vlan
        Match by VLAN Id (VID) in the 802.1Q header.

    -d, --data-link[-protocol], --ethertype
        Match by data link (layer 2) protocol. Can be IPv4, IPv6, ARP, or
        a protocol number.

IP header
    -t, --transport[-protocol], --ip-protocol
        Match by transport (layer 4) protocol. Can be TCP, UDP, ICMP, ICMPv6, or
        a protocol number.
        To further filter TCP packets, an optional list of TCP flags to match can
        be provided. Supported flags are FIN, SYN, RST, PSH, ACK, URG, ECE, and CWR.

    -i, --ip[-address]
        Match source or destination IP address. See NOTE1 above.
        To match by subnet, use CIDR notation with the prefix length.

TCP/UDP header
    -p, --port
        Match source or destination port number. See NOTE1 above.

Encapsulation
    -e, --encap
        This filter also applies to encapsulated inner packets, in addition to the outer
        packet. Supported encapsulation methods are VXLAN, GRE, NVGRE, and IP-in-IP.
        Custom VXLAN port is optional, and defaults to 4789.

Example 1: Ping filter
        pktmon filter add MyPing -i 10.10.10.10 -t ICMP

Example 2: TCP SYN filter for SMB traffic
    pktmon filter add MySmbSyn -i 10.10.10.10 -t TCP SYN -p 445

Example 3: Subnet filter
    pktmon filter add MySubnet -i 10.10.10.0/24
```

## <a name="packet-capture-and-logging"></a>Captura de pacote e registro em log

O monitor de pacotes pode capturar o tráfego de rede com ou sem log de pacotes. Para obter mais informações sobre como capturar o tráfego sem o log de pacotes, verifique a seção contadores de pacotes abaixo. Para capturar e registrar pacotes, adicione o parâmetro **[--ETW]** ao comando Iniciar.

Selecione os componentes a serem monitorados por meio do parâmetro **[-c]** . Ele pode ser todos os componentes, somente NICs ou uma lista de IDs de componentes. O padrão é capturar o tráfego em todos os componentes. Monitorar pacotes ignorados somente com o parâmetro [-d]. O padrão é capturar pacotes de fluxo e ignorados.

Por exemplo, o comando a seguir capturará contadores de pacotes de todos os adaptadores de rede sem pacotes de log:

```PowerShell
C:\Test> pktmon start -c nics
```

No entanto, o comando a seguir capturará somente os pacotes ignorados que passam pelos componentes 4 e 5 e os registrará:

```PowerShell
C:\Test> pktmon start --etw -c 4,5 -d
```

### <a name="packet-logging-capability"></a>Recurso de log de pacotes

- O monitor de pacotes dá suporte a vários modos de log:

  - Circular: novos pacotes substituem os mais antigos quando o tamanho máximo do arquivo é atingido. Esse é o modo de log padrão.
  - Multi-file: um novo arquivo de log é criado quando o tamanho máximo do arquivo é atingido. Os arquivos de log são numerados sequencialmente: PktMon1. ETL, PktMon2. ETL, etc. Aplique esse modo de log para manter todo o log, mas cuidado com a utilização do armazenamento. Observação: Use o carimbo de data/hora de criação do arquivo de cada arquivo de log como uma indicação para um intervalo de tempo específico na captura.
  - Em tempo real: os pacotes são exibidos na tela em tempo real. Nenhum arquivo de log é criado. Use CTRL + C para interromper o monitoramento.
  - Memória: os eventos são gravados em um buffer de memória circular. O tamanho do buffer é especificado por meio do parâmetro **[-s]** . O conteúdo do buffer é gravado em um arquivo de log depois de parar a captura. Use esse modo de log para cenários muito ruidosas para capturar uma grande quantidade de tráfego em uma quantidade muito curta de tempo no buffer de memória. Usando qualquer outro modo de registro em log, algum tráfego pode ser perdido.

- Especifique a quantidade do pacote para fazer logon pelo parâmetro **[-p]** . Registre todo o pacote de cada pacote, independentemente do tamanho, definindo esse parâmetro como 0. O padrão é 128 bytes, que devem incluir os cabeçalhos da maioria dos pacotes.

- Especifique o tamanho do arquivo de log por meio do parâmetro **[-s]** . Esse será o tamanho máximo do arquivo em um modo de log circular antes que o monitor de pacotes comece a substituir os pacotes mais antigos pelos mais recentes. Esse também será o tamanho máximo de cada arquivo no modo de log de vários arquivos antes que o monitor de pacotes crie um novo arquivo para registrar os próximos pacotes. Você também pode usar esse parâmetro para definir o tamanho do buffer para o modo de log de memória.

### <a name="pktmon-start-syntax"></a>Pktmon a sintaxe inicial

```PowerShell
C:\Test> pktmon start help
pktmon start [-c { all | nics | [ids...] }] [-d] [--etw [-p size] [-k keywords]]
             [-f] [-s] [--log-mode {circular | multi-file | real-time | memory}]
    Start packet monitoring.

-c, --components
    Select components to monitor. Can be all components, NICs only, or a
    list of component ids. Defaults to all.

-d, --drop-only
    Only report dropped packets. By default, successful packet propagation
    is reported as well.

ETW Logging
    --etw
        Start a logging session for packet capture.

    -p, --packet-size
        Number of bytes to log from each packet. To always log the entire
        packet, set this to 0. Default is 128 bytes.

    -k, --keywords
        Hexadecimal bitmask (i.e. sum of the below flags) that controls
        which events are logged. Default is 0x012.

        Flags:
        0x001 - Internal Packet Monitor errors.
        0x002 - Information about components, counters and filters.
                This information is added to the end of the log file.
        0x004 - Source and destination information for the first
                packet in NET_BUFFER_LIST group.
        0x008 - Select packet metadata from NDIS_NET_BUFFER_LIST_INFO
                enumeration.
        0x010 - Raw packet, truncated to the size specified in
                [--packet-size] parameter.

    -f, --file-name
        .etl log file. Default is PktMon.etl.

    -s, --file-size
        Maximum log file size in megabytes. Default is 512 MB.

    -l, --log-mode
        Select logging mode. Default is circular.

        circular
            New events overwrite the oldest ones when
            when the maximum file size is reached.

        multi-file
            A new log file is created when the maximum file size is reached.
            Log files are sequentially numbered. PktMon1.etl, PktMon2.etl, etc.

        real-time
            Display events and packets on screen at real time. No log file is created.
            Press Ctrl+C to stop monitoring.

        memory
            Events are written to a circular memory buffer.
            Buffer size is specified in [--file-size] parameter.
            Buffer contents is written to a log file during stop operation.

Example: pktmon start --etw -l real-time
```

## <a name="packet-analysis-and-formatting"></a>Análise e formatação de pacotes

O monitor de pacotes gera arquivos de log no formato ETL. Há várias maneiras de Formatar o arquivo ETL para análise:

- Converta o log em formato de texto (a opção padrão) e analise-o com ferramentas de editor de texto como TextAnalysisTool.NET. Os dados do pacote serão exibidos no formato TCPDump. Siga a guia abaixo para saber como analisar a saída no arquivo de texto.
- Converter o log em formato pcapng para analisá-lo usando o [Wireshark](pktmon-pcapng-support.md)*
- Abra o arquivo ETL com [Monitor de rede](pktmon-netmon-support.md)*

>[!NOTE]
>* Use os hiperlinks acima para saber como analisar e analisar os logs do monitor de pacotes no **Wireshark** e **Monitor de rede**.

### <a name="pktmon-format-syntax"></a>Sintaxe de formato Pktmon

```PowerShell
C:\Test> pktmon format help
pktmon format log.etl [-o log.txt] [-b] [-v [level]] [-x] [-e] [-l [port]
    Convert log file to text format.

-o, --out
    Name of the formatted text file.

-s, --stats-only
    Display log file statistical information.

Network packet formatting options

    -b, --brief
        Abbreviated packet format.

    -v, --verbose
        Verbosity level [1..3].

    -x, --hex
        Hexadecimal format.

    -e, --no-ethernet
        Don't print ethernet header.

    -l, --vxlan
        Custom VXLAN port.


Example: pktmon format C:\tmp\PktMon.etl

C:\Test> pktmon pcapng help
pktmon pcapng log.etl [-o log.pcapng]
    Convert log file to pcapng format.
    Dropped packets are not included by default.

-o, --out
    Name of the formatted pcapng file.

-d, --drop-only
    Convert dropped packets only.

-c, --component-id
    Filter packets by a specific component ID.

Example: pktmon pcapng C:\tmp\PktMon.etl -d -c nics
```

### <a name="analyze-packet-monitor-output"></a>Analisar saída do monitor de pacotes

O monitor de pacotes captura um instantâneo do pacote por cada componente da pilha de rede. Da mesma forma, haverá vários instantâneos de cada pacote (representados na imagem abaixo, nas linhas da caixa azul).
Cada um desses instantâneos de pacote é representado por duas linhas (caixas vermelhas e verdes). Há pelo menos uma linha que inclui alguns dados sobre a instância do pacote, começando com o carimbo de data/hora. Logo após, há pelo menos uma linha (em negrito na imagem abaixo) para mostrar o pacote bruto analisado no formato de texto (sem um carimbo de data/hora); pode ser várias linhas se o pacote for encapsulado, como o pacote na caixa verde.

<center>

:::image type="content" source="media/pktmon-log-example.png" alt-text="Exemplo de saída de log txt do monitor de pacotes" border="false":::

</center>

Para correlacionar todos os instantâneos dos mesmos pacotes, monitore os valores PktGroupId e PktNumber (realçado em amarelo); todos os instantâneos do mesmo pacote devem ter esses dois valores em comum. O valor de aparência (realçado em azul) atua como um contador para cada instantâneo subsequente do mesmo pacote. Por exemplo, o primeiro instantâneo do pacote (em que o pacote apareceu pela primeira vez na pilha de rede) tem o valor 1 para aparência, o próximo instantâneo tem o valor 2 e assim por diante.

Cada instantâneo de pacote tem uma ID de componente (sublinhada na imagem acima), indicando o componente associado ao instantâneo. Para resolver o nome do componente e os parâmetros, pesquise essa ID de componente na lista de componentes na parte inferior do arquivo de log. Uma parte da tabela componentes é mostrada na imagem abaixo, realçando "componente 1" em amarelo (esse era o componente em que o último instantâneo foi capturado).
Os componentes com 2 bordas relatarão 2 instantâneos em cada borda (como os instantâneos com a aparência 3 e a aparência 4, por exemplo, na imagem acima).

Na parte inferior de cada arquivo de log, a lista de filtros é apresentada conforme mostrado na imagem abaixo (realçada em azul). Cada filtro exibe os parâmetros especificados (protocolo ICMP no exemplo abaixo) e zeros para o restante dos parâmetros.

<center>

:::image type="content" source="media/pktmon-log-example-components.png" alt-text="Exemplo de componentes de saída de log txt do monitor de pacotes":::

</center>

Para pacotes ignorados, a palavra "drop" aparece antes de qualquer uma das linhas que representam o instantâneo onde o pacote foi Descartado. Cada pacote Descartado também fornece um valor de dropReason. Esse parâmetro dropReason fornece uma breve descrição do motivo para soltar o pacote; por exemplo, incompatibilidade de MTU, VLAN filtrada, etc.

<center>

:::image type="content" source="media/dropped-packet-log-example.png" alt-text="Exemplo de um log de pacote Descartado":::

</center>

## <a name="packet-counters"></a>Contadores de pacotes

Os contadores de monitor de pacotes fornecem uma exibição de alto nível do tráfego de rede em toda a pilha de rede sem a necessidade de analisar um log, o que pode ser um processo caro. Examine os padrões de tráfego consultando contadores de pacotes com **contadores pktmon** depois de iniciar a captura do monitor de pacotes. Redefina os contadores para zero usando **pktmon Reset** ou pare de monitorar todos juntos usando **pktmon Stop**.

- Os contadores são organizados por pilhas de associação com adaptadores de rede na parte superior e protocolos na parte inferior.
- TX/RX: os contadores são separados em duas colunas para as direções enviar (TX) e receber (RX).  
- Bordas: os componentes relatam a propagação de pacotes quando um pacote está ultrapassando o limite do componente (borda). Cada componente pode ter uma ou mais bordas. Os drivers de miniporta normalmente têm borda superior única, os protocolos têm borda inferior única e os drivers de filtro têm bordas superiores e inferiores.  
- Quedas: os contadores de remoção de pacotes estão sendo relatados na mesma tabela.

No exemplo a seguir, uma nova captura foi iniciada, então o comando **pktmon Counters** foi usado para consultar os contadores antes da interrupção da captura. Os contadores mostram um único pacote que o torna fora da pilha de rede, começando da camada de protocolo até o adaptador de rede física e sua resposta volta na outra direção. Se o ping ou a resposta estava ausente, é fácil detectá-lo por meio dos contadores.

<center>

:::image type="content" source="media/pktmon-counters-with-perfect-flow.png" alt-text="Exemplo de um contador de pacotes com fluxo perfeito" border="false":::

</center>

No exemplo a seguir, os descartes são relatados na coluna "Counter". Recupere a última razão de descarte para cada componente solicitando dados de contadores no formato JSON usando **contadores pktmon--JSON** ou analise o log de saída para obter informações mais detalhadas.

<center>

:::image type="content" source="media/pktmon-counters-drop-example.png" alt-text="Exemplo de um contador de pacotes com um pacote Descartado" border="false":::

</center>

Conforme mostrado nesses exemplos, os contadores podem fornecer muitas informações por meio de um diagrama que pode ser analisado apenas com uma aparência rápida.

### <a name="pktmon-counters-syntax"></a>Sintaxe de contadores de Pktmon

```PowerShell
C:\Test> pktmon counters help
pktmon [comp] counters [-t { all | drop | flow }] [-z] [--json]
    Display current per-component counters.

-t, --counter-type
    Select which types of counters to show.
    Supported values are all counters (default), drops only, or flows only.

-z, --show-zeros
    Show counters that are zero in both directions.

-i, --show-hidden
    Show components that are hidden by default.

--json
    Output the counters in JSON format.
```

## <a name="networking-stack-layout"></a>Layout de pilha de rede

Examine o layout da pilha de rede por meio da **lista de pktmon** de comando.

:::image type="content" source="media/pktmon-networking-stack-example.png" alt-text="Exemplo de layout de pilha de rede" border="false":::

O comando mostra os componentes de rede (drivers) organizados por associações de adaptadores.

Uma associação típica consiste em:

- Uma única placa de interface de rede (NIC)
- Alguns (possivelmente zero) drivers de filtro
- Um ou mais drivers de protocolo (TCP/IP ou outros)

Cada componente é identificado exclusivamente por uma ID de componente de monitor de pacotes, que é usada para direcionar componentes individuais para monitoramento.

>[!NOTE]
>As IDs não são persistentes e podem ser alteradas entre as reinicializações e as reinicializações do driver do monitor de pacotes.

### <a name="pktmon-list-syntax"></a>Sintaxe da lista de Pktmon

```powershell
C:\Test> pktmon list help
pktmon [comp] list
    List all active components.

-i, --show-hidden
    Show components that are hidden by default.

--json
    Output the list in JSON format.
```