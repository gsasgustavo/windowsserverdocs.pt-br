---
title: Aprimorar o desempenho de um servidor de arquivos com o SMB Direct
description: Descreve o recurso SMB Direct no Windows Server 2012 R2, no Windows Server 2012 e no Windows Server 2016.
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5f9f34e4491d8cd4455fcb5b09b30847f6f66887
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954713"
---
# <a name="smb-direct"></a>SMB Direct

>Aplica-se a: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

O Windows Server 2012 R2, o Windows Server 2012 e o Windows Server 2016 incluem um recurso chamado SMB Direct, que dá suporte ao uso de adaptadores de rede que têm a capacidade RDMA (Acesso Remoto Direto à Memória). Os adaptadores de rede com RDMA podem funcionar a toda a velocidade com latência muito baixa, usando muito pouco da CPU. Para cargas de trabalho como o Hyper-V ou o Microsoft SQL Server, isso permite que um servidor de arquivos remoto se pareça com um armazenamento local. O SMB Direct inclui:

- Maior taxa de transferência: Aproveita a taxa de transferência total de redes de alta velocidade em que os adaptadores de rede coordenam a transferência de grandes volumes de dados em velocidade da linha.
- Baixa latência: Fornece respostas extremamente rápidas às solicitações de rede e, como resultado, faz com que o armazenamento de arquivos remoto pareça estar diretamente conectado ao armazenamento em bloco.
- Baixa utilização da CPU: Usa menos ciclos da CPU ao transferir dados pela rede, o que disponibiliza mais energia para os aplicativos para servidor.

O SMB Direct é configurado automaticamente pelo Windows Server 2012 R2 e pelo Windows Server 2012.

## <a name="smb-multichannel-and-smb-direct"></a>SMB Multichannel e SMB Direct

SMB Multichannel é o recurso responsável pela detecção de capacidades RDMA de adaptadores de rede para habilitar o SMB Direct. Sem o SMB Multichannel, o SMB usa o TCP/IP normal com os adaptadores de rede compatíveis com RDMA (todos os adaptadores de rede fornecem uma pilha de TCP/IP juntamente com a nova pilha RDMA).

Com o SMB Multichannel, o SMB detecta se um adaptador de rede tem a capacidade RDMA e cria várias conexões RDMA para essa única sessão (duas por interface). Assim, o SMB pode usar a alta taxa de transferência, a baixa latência e a baixa utilização de CPU oferecidas por adaptadores de rede compatíveis com RDMA. Ele também oferecerá tolerância a falhas, se você estiver usando várias interfaces RDMA.

>[!NOTE]
>Não agrupe adaptadores de rede compatíveis com RDMA se pretender usar a capacidade RDMA dos adaptadores de rede. Quando agrupados, os adaptadores de rede não dão suporte ao RDMA.
>Depois que for criada pelo menos uma conexão de rede RDMA, a conexão TCP/IP usada para a negociação de protocolo original não será mais usada. No entanto, a conexão TCP/IP será mantida, caso as conexões de rede RDMA falhem.

## <a name="requirements"></a>Requisitos

O SMB Direct requer o seguinte:

- Pelo menos dois computadores que executam o Windows Server 2012 R2 ou o Windows Server 2012
- Um ou mais adaptadores de rede com capacidade RDMA.

### <a name="considerations-when-using-smb-direct"></a>Considerações sobre o uso do SMB Direct

- Você pode usar o SMB Direct em um cluster de failover; entretanto, certifique-se de que as redes de cluster usadas para o acesso de clientes são adequadas para o SMB Direct. O cluster de failover dá suporte ao uso de várias redes para acesso de clientes, juntamente com adaptadores de rede compatíveis com RSS (Receive Side Scaling) e com RDMA.
- Você pode usar o SMB Direct no sistema operacional de gerenciamento Hyper-V para dar suporte ao uso do Hyper-V no SMB, e para fornecer armazenamento para uma máquina virtual que use a pilha de armazenamento do Hyper-V. No entanto, os adaptadores de rede compatíveis com RDMA não são diretamente expostos ao cliente Hyper-V. Se você conectar um adaptador de rede compatível com RDMA a um comutador virtual, os adaptadores de rede virtual do comutador não serão compatíveis com RDMA.
- Se você desabilitar o SMB Multichannel, o SMB Direct também será desabilitado. Como o SMB Multichannel detecta capacidades de adaptadores de rede e determina se um adaptador de rede é compatível com RDMA, o SMB Direct não pode ser usado pelo cliente quando o SMB Multichannel está desabilitado.
- SMB Direct não é compatível com o Windows RT. O SMB Direct exige suporte para adaptadores de rede compatíveis com RDMA, que está disponível somente no Windows Server 2012 R2 e no Windows Server 2012.
- Não há suporte para SMB Direct em versões inferiores do Windows Server. Há suporte apenas no Windows Server 2012 R2 e no Windows Server 2012.

## <a name="enabling-and-disabling-smb-direct"></a>Habilitando e desabilitando o SMB Direct

O SMB Direct é habilitado por padrão quando o Windows Server 2012 R2 ou o Windows Server 2012 está instalado. O cliente SMB detecta e usa automaticamente várias conexões de rede quando uma configuração apropriada é identificada.

### <a name="disable-smb-direct"></a>Desabilitar SMB Direct

Normalmente, não será necessário desabilitar o SMB Direct; contudo, você pode desabilitá-lo executando um dos seguintes scripts do Windows PowerShell.

Para desabilitar o RDMA para uma interface específica, digite:

```PowerShell
Disable-NetAdapterRdma <name>
```

Para desabilitar o RDMA para todas as interfaces, digite:

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Disabled
```

Quando você desabilita o RDMA no cliente ou no servidor, os sistemas não podem usá-lo. *Network Direct* é o nome interno para o Windows Server 2012 R2 e o suporte à rede básica do Windows Server 2012 para interfaces RDMA.

### <a name="re-enable-smb-direct"></a>Reabilitar o SMB Direct

Depois de desabilitar o RDMA, é possível reabilitá-lo executando um dos scripts do Windows PowerShell a seguir.

Para reabilitar o RDMA para uma interface específica, digite:

```PowerShell
Enable-NetAdapterRDMA <name>
```

Para reabilitar o RDMA para todas as interfaces, digite:

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Enabled
```

É necessário habilitar o RDMA no cliente e no servidor para começar a usá-lo novamente.

## <a name="test-performance-of-smb-direct"></a>Testar o desempenho do SMB Direct

Você pode testar o funcionamento do desempenho usando um dos procedimentos a seguir.

### <a name="compare-a-file-copy-with-and-without-using-smb-direct"></a>Compare cópias do arquivo com e sem usar o SMB Direct

Faça assim para medir o aumento na taxa de transferência do SMB Direct:

1. Configurar o SMB Direct
2. Meça o tempo necessário para executar uma cópia de um arquivo grande usando o SMB Direct.
3. Desabilite o RDMA no adaptador de rede, consulte [Enabling and disabling SMB Direct](#enabling-and-disabling-smb-direct).
4. Meça o tempo necessário para executar uma cópia de um arquivo grande sem usar o SMB Direct.
5. Reabilite o RDMA no adaptador de rede e compare os dois resultados.
6. Para evitar o impacto do armazenamento em cache, execute o seguinte procedimento:
    1. Copie uma grande quantidade de dados (mais dados do que a memória é capaz de tratar).
    2. Copie os dados duas vezes, com a primeira cópia como um treino e depois medindo o tempo da segunda cópia.
    3. Reinicie o servidor e o cliente antes de cada teste para garantir que eles estejam operando em condições semelhantes.

### <a name="fail-one-of-multiple-network-adapters-during-a-file-copy-with-smb-direct"></a>Falhar um de vários adaptadores de rede durante a cópia de um arquivo com o SMB Direct

Faça assim para confirmar a capacidade de failover do SMB Direct:

1. Verifique se o SMB Direct está funcionando em uma configuração de vários adaptadores de rede.
2. Execute a cópia de um arquivo grande. Enquanto a cópia está em execução, simule uma falha de um dos caminhos de rede desconectando um dos cabos (ou desabilitando um dos adaptadores de rede).
3. Confirme se a cópia do arquivo continua usando um dos adaptadores de rede restantes e se não há erros de cópia do arquivo.

>[!NOTE]
>Para evitar falhas em uma carga de trabalho que não utilize SMB Direct, certifique-se de que não haja outras cargas de trabalho usando o caminho de rede desconectado.

## <a name="more-information"></a>Mais informações

- [Visão geral do Protocolo SMB](file-server-smb-overview.md)
- [Como aumentar a disponibilidade do servidor, do armazenamento e da rede: visão geral do cenário](</previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [Implantar o Hyper-V no SMB](</previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
