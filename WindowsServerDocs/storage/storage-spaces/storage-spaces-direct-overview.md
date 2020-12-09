---
title: Visão geral de Espaços de Armazenamento Diretos
ms.author: cosdar
manager: dongill
ms.topic: article
author: cosmosdarwin
ms.date: 07/24/2020
ms.assetid: 8bd0d09a-0421-40a4-b752-40ecb5350ffd
description: Uma visão geral do Espaços de Armazenamento Diretos, um recurso do Windows Server e Azure Stack HCI que permite a você agrupar servidores com armazenamento interno em uma solução de armazenamento definida por software.
ms.localizationpriority: medium
ms.openlocfilehash: 726bb42c2f652bf6cd6165adb0afed0237040aaf
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96864865"
---
# <a name="storage-spaces-direct-overview"></a>Visão geral de Espaços de Armazenamento Diretos

>Aplica-se a: Azure Stack HCI, Windows Server 2019, Windows Server 2016

O recurso Espaços de Armazenamento Diretos usa servidores padrão do setor com unidades conectadas localmente para criar um armazenamento definido pelo software altamente disponível e escalonável com custo menor do que o de matrizes de SAN ou NAS tradicionais. Sua arquitetura convergida ou hiperconvergente simplifica radicalmente a aquisição e a implantação, enquanto recursos como cache, camadas de armazenamento e codificação de eliminação, junto com as inovações de hardware mais recentes, como a rede RDMA e unidades de NVMe, proporcionam eficiência e desempenho incomparáveis.

Espaços de Armazenamento Diretos está incluído nas compilações [Azure Stack HCI](/azure-stack/hci/), windows Server 2019 datacenter, windows Server 2016 datacenter e [Windows Server Insider Preview](https://insider.windows.com/for-business-getting-started-server/).

Para outros aplicativos de espaços de armazenamento, como clusters SAS compartilhados e servidores autônomos, consulte [visão geral de espaços de armazenamento](overview.md). Se você estiver procurando informações sobre como usar espaços de armazenamento em um PC com Windows 10, consulte [espaços de armazenamento no Windows 10](https://support.microsoft.com/help/12438/windows-10-storage-spaces).

| Descrição | Documentação |
|--|--|
| **Noções básicas**<br><ul><li>Visão geral (você está aqui)</li><li>[Noções básicas sobre o cache](understand-the-cache.md)</li><li>[Tolerância a falhas e eficiência de armazenamento](storage-spaces-fault-tolerance.md)<li>[Considerações de simetria de unidade](drive-symmetry-considerations.md)</li><li>[Entender e monitorar a ressincronização de armazenamento](understand-storage-resync.md)</li><li>[Noções básicas de quorum de cluster e de pool](understand-quorum.md)</li><li>[Conjuntos de cluster](cluster-sets.md)</li> | **Plano**<br><ul><li>[Requisitos de hardware](storage-spaces-direct-hardware-requirements.md)</li><li>[Usar o cache de leitura na memória de CSV](csv-cache.md)</li><li>[Escolher unidades](choosing-drives.md)</li><li>[Planejar volumes](plan-volumes.md)</li><li>[Usar clusters de VM convidada](storage-spaces-direct-in-vm.md)</li><li>[Recuperação de desastres](storage-spaces-direct-disaster-recovery.md)</li> |
| **Implantar**<br><ul><li>[Implantar Espaços de Armazenamento Diretos](deploy-storage-spaces-direct.md)</li><li>[Criar volumes](create-volumes.md)</li><li>[Resiliência aninhada](nested-resiliency.md)</li><li>[Configurar quorum](../../failover-clustering/manage-cluster-quorum.md)</li><li>[Atualizar um cluster de Espaços de Armazenamento Diretos para o Windows Server 2019](upgrade-storage-spaces-direct-to-windows-server-2019.md)</li><li>[Compreender e implantar memória persistente](deploy-pmem.md)</li> | **Gerenciar**<br><ul><li>[Gerenciar com o Centro de Administração do Windows](../../manage/windows-admin-center/use/manage-hyper-converged.md)</li><li>[Adicionar servidores ou unidades](add-nodes.md)</li><li>[Colocar um servidor offline para manutenção](maintain-servers.md)</li><li>[Remover servidores](remove-servers.md)</li><li>[Estender volumes](resize-volumes.md)</li><li>[Excluir volumes](delete-volumes.md)</li><li>[Atualizar firmware da unidade](../update-firmware.md)</li><li>[Histórico de desempenho](performance-history.md)</li><li>[Delimitar a alocação de volumes](delimit-volume-allocation.md)</li><li>[Usar Azure Monitor em um cluster hiperconvergente](configure-azure-monitor.md)</li> |
| **Solução de problemas**<br><ul><li>[Cenários de solução de problemas](troubleshooting-storage-spaces.md)</li><li>[Solucionar problemas de integridade e Estados operacionais](storage-spaces-states.md)</li><li>[Coletar dados de diagnóstico com Espaços de Armazenamento Diretos](data-collection.md)</li><li>[Gerenciamento de integridade de memória da classe de armazenamento](Storage-class-memory-health.md)</li> | **Postagens recentes no blog**<br><ul><li>[13,7 milhões IOPS com Espaços de Armazenamento Diretos: o novo registro do setor para a infraestrutura hiperconvergente](https://techcommunity.microsoft.com/t5/storage-at-microsoft/the-new-hci-industry-record-13-7-million-iops-with-windows/ba-p/428314)</li><li>[Infraestrutura hiperconvergente no Windows Server 2019-o relógio de contagem regressiva começa agora!](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)</li><li>[Cinco anúncios grandes do Windows Server Summit](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)</li><li>[10.000 Espaços de Armazenamento Diretos de clusters e contagem...](https://techcommunity.microsoft.com/t5/storage-at-microsoft/storage-spaces-direct-10-000-clusters-and-counting/ba-p/428185)</li></ul> |

## <a name="videos"></a>Vídeos

**Visão geral de vídeo rápido (5 minutos)**

> [!Video https://www.youtube-nocookie.com/embed/raeUiNtMk0E]

**Espaços de Armazenamento Diretos no Microsoft Ignite 2018 (1 hora)**

> [!Video https://www.youtube-nocookie.com/embed/5kaUiW3qo30]

**Espaços de Armazenamento Diretos no Microsoft Ignite 2017 (1 hora)**

> [!Video https://www.youtube-nocookie.com/embed/YDr2sqNB-3c]

**Evento de inicialização no Microsoft Ignite 2016 (1 hora)**

> [!Video https://www.youtube-nocookie.com/embed/LK2ViRGbWs]

## <a name="key-benefits"></a>Principais benefícios

| Imagem | Descrição |
|--|--|
| ![Simplicidade](media/storage-spaces-direct-in-windows-server-2016/simplicity-icon.png) | **Simplicidade.** Passe de servidores padrão do setor que executam o Windows Server 2016 para seu primeiro cluster de Espaços de Armazenamento Diretos em menos de 15 minutos. Para usuários do System Center, a implantação é apenas uma caixa de seleção. |
| ![Desempenho inigualável](media/storage-spaces-direct-in-windows-server-2016/performance-icon.png) | **Desempenho inigualável.** Se todos os flash ou híbrida, espaços de armazenamento Direct facilmente exceder [150.000 misto 4K aleatório IOPS por servidor](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) com consistente e de baixa latência graças à sua arquitetura de hipervisor interno, seu interno cache de leitura/gravação e suporte para unidades de NVMe ponta montadas diretamente no barramento PCIe. |
| ![Tolerância a falhas](media/storage-spaces-direct-in-windows-server-2016/fault-tolerance-icon.png) | **Tolerância a falhas.** A resiliência interna manuseia falhas de unidade, servidor ou componente com disponibilidade contínua. Implantações maiores também podem ser configuradas para [a tolerância a falhas de chassis e do rack](../../failover-clustering/fault-domains.md). Quando o hardware falhar, basta trocá-lo; o software se repara sozinho, sem etapas de gerenciamento complicadas. |
| ![Eficiência de recursos](media/storage-spaces-direct-in-windows-server-2016/efficiency-icon.png) | **Eficiência de recursos.** A codificação de eliminação oferece eficiência de armazenamento até 2,4 x maior, com inovações exclusivas como Códigos de reconstrução local e camadas em tempo real ReFS para expandir esses ganhos a unidades de disco rígido e cargas de trabalho ativas/passivas mistas, tudo isso enquanto o consumo da CPU é minimizado para devolver recursos para onde eles são mais necessários – nas VMs. |
| ![Capacidade de gerenciamento](media/storage-spaces-direct-in-windows-server-2016/manageability-icon.png) | **Capacidade de gerenciamento**. Use [Controles QoS de armazenamento](../storage-qos/storage-qos-overview.md) para manter VMs ocupadas excessivamente na verificação dos limites mínimo e máximo de IOPS por VM. O [serviço de integridade](../../failover-clustering/health-service-overview.md) oferece monitoramento e alertas internos contínuos e novas APIs facilitam a coleta de métricas de capacidade e desempenho avançadas em todo o cluster. |
| ![Escalabilidade](media/storage-spaces-direct-in-windows-server-2016/scalability-icon.png) | **Escalabilidade**. Tenha até 16 servidores e mais de 400 unidades para até 1 petabyte (1.000 terabytes) de armazenamento por cluster. Para escalar horizontalmente, basta adicionar unidades ou mais servidores. O recurso Espaços de Armazenamento Diretos integrará automaticamente novas unidades e começará a usá-las. O desempenho e a eficiência de armazenamento melhoram de maneira previsível grande escala. |

## <a name="deployment-options"></a>Opções de implantação

O recurso Espaços de Armazenamento Diretos foi criado para duas opções de implantação distintas:

### <a name="converged"></a>Convergido

**Armazenamento e computação em clusters separados.** A opção de implantação convergente, também conhecida como "desagregada", dispõe um SoFS (Servidor de Arquivos de Escalabilidade Horizontal) em camadas sobre Espaços de Armazenamento Diretos para oferecer NAS por meio de compartilhamentos de arquivos SMB3. Isso permite o dimensionamento de computação/carga de trabalho independentemente do cluster de armazenamento, essencial para implantações em maior escala, como o IaaS (Infraestrutura como Serviço) Hyper-V para provedores de serviços e empresas.

![Os Espaços de Armazenamento Diretos servem para armazenamento usando o recurso Servidor de Arquivos de Escalabilidade Horizontal para VMs do Hyper-V em outro servidor ou cluster](media/storage-spaces-direct-in-windows-server-2016/converged-minimal.png)

### <a name="hyper-converged"></a>Hiperconvergentes

**Um cluster para computação e armazenamento.** A opção de implantação hiperconvergente executa máquinas virtuais Hyper-V ou bancos de dados do SQL Server diretamente nos servidores que oferecem o armazenamento, armazenando seus arquivos em volumes locais. Isso acaba com a necessidade de configurar permissões e acesso ao servidor de arquivos de configuração e reduz os custos de hardware para empresas de pequeno a médio porte ou implantações do escritório remoto/filial. Consulte [implantar espaços de armazenamento diretos](deploy-storage-spaces-direct.md).

![Espaços de Armazenamento Diretos servem de armazenamento para VMs do Hyper-V no mesmo cluster](media/storage-spaces-direct-in-windows-server-2016/hyper-converged-minimal.png)

## <a name="how-it-works"></a>Como ele funciona

O recurso Espaços de Armazenamento Diretos é a evolução do Espaços de Armazenamento, introduzido pela primeira vez no Windows Server 2012. Ele usa muitos dos recursos que você conhece hoje no Windows Server, como Clustering de Failover, o sistema de arquivos CSV (Volume Compartilhado Clusterizado), protocolo SMB 3 e, claro, o Espaços de Armazenamento. Ele também introduz uma nova tecnologia, mais notavelmente Barramento de armazenamento de software.

Eis uma visão geral da pilha de Espaços de Armazenamento Diretos:

![Pilha de Espaços de Armazenamento Diretos](media/storage-spaces-direct-in-windows-server-2016/converged-full-stack.png)

**Hardware de rede.** O recurso Espaços de Armazenamento Diretos usa SMB3, incluindo o SMB Direct e o SMB Multichannel por Ethernet para comunicação entre servidores. É altamente recomendável ter mais de 10 GbE com RDMA (Acesso Remoto Direto à Memória), iWARP ou RoCE.

**Hardware de armazenamento.** De 2 a 16 servidores com unidades SATA, SAS ou NVMe conectadas localmente. Cada servidor deve ter pelo menos 2 unidades de estado sólido e pelo menos 4 unidades adicionais. Os dispositivos SATA e SAS devem ficar atrás de um HBA (adaptador de barramento do host) e expansor SAS. Recomendamos as plataformas meticulosamente projetadas e amplamente validadas dos nossos parceiros (em breve).

**Clustering de failover.** O recurso interno de clustering do Windows Server é usado para conectar os servidores.

**Barramento de armazenamento de software.** O Barramento de Armazenamento de Software é novo no recurso Espaços de Armazenamento Diretos. Ele abrange o cluster e estabelece uma malha de armazenamento definida pelo software por meio do qual todos os servidores podem ver todas as unidades locais uns dos outros. Você pode considerá-lo quanto for substituir o cabeamento caro e restritivo do Fibre Channel ou do SAS Compartilhado.

**Cache da Camada do Barramento de Armazenamento.** O Barramento de Armazenamento de Software associa dinamicamente as unidades mais rápidas presentes (por exemplo, SSD) às unidades mais lentas (por exemplo, HDDs) para fornecer o caching de leitura/gravação do lado do servidor que acelera a E/S e aumenta a taxa de transferência.

**Pool de armazenamento.** A coleção de unidades que forma a base do Espaços de Armazenamento é denominada pool de armazenamento. Ele é criado automaticamente e todas as unidades elegíveis são descobertas automaticamente e adicionadas a ele. É altamente recomendável que você use um pool por cluster, com as configurações padrão. Leia [Deep Dive into the Storage Pool](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deep-dive-the-storage-pool-in-storage-spaces-direct/ba-p/425959) para saber mais.

**Espaços de armazenamento.** Os espaços de armazenamento fornecem tolerância a falhas para "discos" virtuais usando [espelhamento, codificação de apagamento ou ambos](storage-spaces-fault-tolerance.md). Você pode pensar nele como um RAID distribuído e definido pelo software que usa as unidades no pool. Em espaços de armazenamento direto, esses discos virtuais normalmente têm resiliência para duas unidades ou servidor falhas simultâneas (por exemplo, 3 vias espelhamento, com cada cópia de dados em um servidor diferente) embora chassi e tolerância a falhas de rack também está disponível.

**ReFS (sistema de arquivos resiliente).** O ReFS é um sistema de arquivos premier desenvolvido especificamente para virtualização. Ele inclui acelerações significativas para operações de arquivo .vhdx como criação, expansão, mesclagem de ponto de verificação e somas de verificação internas para detectar e corrigir erros de bit. Ele também apresenta camadas em tempo real que rotacionam dados entre camadas de armazenamento "quentes" e "frias" em tempo real com base na utilização.

**Volumes compartilhados do cluster.** O sistema de arquivos CSV unifica todos os volumes ReFS em um único namespace acessível por meio de qualquer servidor para que cada servidor e cada volume pareçam e ajam como são montados localmente.

**Servidor de Arquivos de Escalabilidade Horizontal.** Essa camada final é necessária somente em implantações convergentes. Ela oferece acesso a arquivo remoto usando o protocolo de acesso SMB3 aos clientes, como outro cluster que executa o Hyper-V pela rede, transformando efetivamente Espaços de Armazenamento Diretos em NAS.

## <a name="customer-stories"></a>Relatos de clientes

Há [mais de 10.000 clusters](https://techcommunity.microsoft.com/t5/storage-at-microsoft/storage-spaces-direct-10-000-clusters-and-counting/ba-p/428185) em todo o mundo executando espaços de armazenamento diretos. Organizações de todos os tamanhos, de pequenas empresas implantando apenas dois nós, a grandes empresas e governos implantando centenas de nós dependem de Espaços de Armazenamento Diretos para seus aplicativos e infraestrutura críticos.

Visite [Microsoft.com/HCI](https://www.microsoft.com/hci) para ler suas histórias:

[![Logotipo da grade de clientes](media/storage-spaces-direct-in-windows-server-2016/customer-stories.png)](https://www.microsoft.com/hci)

## <a name="management-tools"></a>Ferramentas de gerenciamento

As seguintes ferramentas podem ser usadas para gerenciar e/ou monitorar Espaços de Armazenamento Diretos:

| Nome | Gráfico ou linha de comando? | Pago ou incluído? |
|-----------------|----------------------------|-------------------|
| [Windows Admin Center](../../manage/windows-admin-center/overview.md)     | Gráfico    | Incluso |
| Gerenciador do Servidor & Gerenciador de Cluster de Failover                                 | Gráfico    | Incluso |
| Windows PowerShell                                                        | Linha de comando | Incluso |
| [System Center Virtual Machine Manager (SCVMM)](/system-center/vmm/s2d) <br>& [Operations Manager (SCOM)](https://www.microsoft.com/download/details.aspx?id=54700) | Gráfico    | Pago     |

## <a name="get-started"></a>Introdução

Experimente Espaços de Armazenamento Diretos [no Microsoft Azure](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB), ou baixe uma cópia de avaliação de 180 dias licenciados do Windows Server em [Avaliações do Windows Server](https://go.microsoft.com/fwlink/?linkid=842602).

## <a name="additional-references"></a>Referências adicionais

- [Tolerância a falhas e eficiência de armazenamento](storage-spaces-fault-tolerance.md)
- [Réplica de armazenamento](../storage-replica/storage-replica-overview.md)
- [Blog do armazenamento no Microsoft](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)
- [Taxa de transferência de Espaços de Armazenamento Diretos com iWARP](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) (blog do TechNet)
- [Novidades em Clustering de Failover no Windows Server](../../failover-clustering/whats-new-in-failover-clustering.md)
- [Qualidade de serviço do armazenamento](../storage-qos/storage-qos-overview.md)
- [Suporte do Windows IT Pro](https://www.microsoft.com/itpro/windows/support)
