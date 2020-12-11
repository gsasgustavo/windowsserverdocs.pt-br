---
description: 'Saiba mais sobre: o que há de novo na eliminação de duplicação de dados'
ms.assetid: d11acbc2-40c6-4ab2-9514-2bc3ad81499a
title: Novidades na Eliminação de Duplicação de Dados
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 04/17/2019
ms.openlocfilehash: a33a248c8fce180b6ffe3de335fa876829ae05a9
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97048464"
---
# <a name="whats-new-in-data-deduplication"></a>Novidades na Eliminação de Duplicação de Dados

> Aplica-se a: Windows Server 2019, Windows Server 2016, Windows Server (canal semestral)

A [eliminação de duplicação de dados](overview.md) no Windows Server foi otimizada para ser altamente funcional, flexível e gerenciável em escala de nuvem privada. Para obter mais informações sobre a pilha de armazenamento definida pelo software no Windows Server, consulte [o que há de novo no armazenamento no Windows Server](../whats-new-in-storage.md).

A eliminação de duplicação de dados tem os seguintes aprimoramentos no Windows Server 2019:

| Funcionalidade | Novo ou atualizado | Descrição |
|---------------|----------------|-------------|
| Suporte a ReFS  | Novo            | Armazene até 10 vezes mais dados no mesmo volume com eliminação de duplicação e compactação para o sistema de arquivos ReFS. (É [apenas um clique](https://www.youtube.com/watch?v=PRibTacyKko&feature=youtu.be) para ativar com o centro de administração do Windows.) O repositório de partes de tamanho variável com compactação opcional maximiza as taxas de economia, enquanto a arquitetura de pós-processamento multi-threaded mantém o impacto do desempenho mínimo. Dá suporte a volumes de até 64 TB e eliminará a duplicação dos primeiros 4 TB de cada arquivo.|

A eliminação de duplicação de dados tem os seguintes aprimoramentos a partir do Windows Server 2016:

| Funcionalidade | Novo ou atualizado | Descrição |
|---------------|----------------|-------------|
| [Suporte a volumes grandes](whats-new.md#large-volume-support) | Atualizado | Antes do Windows Server 2016, os volumes tinham que ser dimensionados especificamente para a variação esperada e os tamanhos de volume acima de 10 TB não eram bons candidatos para eliminação de duplicação. No Windows Server 2016, a Eliminação de Duplicação de Dados dá suporte a tamanhos de volume de até 64 TB. |
| [Suporte para arquivos grandes](whats-new.md#large-file-support) | Atualizado | Antes do Windows Server 2016, arquivos com tamanho próximo a 1 TB não eram bons candidatos para eliminação de duplicação. No Windows Server 2016, arquivos com até 1 TB têm suporte completo. |
| [Suporte ao Nano Server](whats-new.md#nano-server-support) | Novo | A Eliminação de Duplicação de Dados está disponível e tem suporte completo na nova opção de implantação do Nano Server para Windows Server 2016. |
| [Suporte de backup simplificado](whats-new.md#simple-backup-support) | Novo | O Windows Server 2012 R2 dava suporte a Aplicativos de Backup Virtualizado, como o [Data Protection Manager](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) da Microsoft por meio de uma série de etapas de configuração manual. O Windows Server 2016 adicionou um novo tipo de uso padrão (backup) para implantação perfeita da Eliminação de Duplicação de Dados para Aplicativos de Backup Virtualizado.|
| [Suporte a atualizações do sistema operacional de cluster sem interrupção](whats-new.md#cluster-upgrade-support) | Novo | A Eliminação de Duplicação de Dados dá suporte completo ao novo recurso [Atualização sem Interrupção do SO de Cluster](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md) do Windows Server 2016. |

## <a name="support-for-large-volumes"></a><a name="large-volume-support"></a>Suporte a volumes grandes

**Qual é o valor agregado desta alteração?**
Para obter o melhor desempenho da Eliminação de Duplicação de Dados no Windows Server 2012 R2, os volumes devem ser dimensionados adequadamente para garantir que o trabalho de Otimização possa acompanhar a taxa de alterações de dados ou “variação”. Normalmente, isso significa que a Eliminação de Duplicação de Dados é eficaz somente em volumes de até 10 TB, dependendo dos padrões de gravação da carga de trabalho.

No Windows Server 2016, a Eliminação de Duplicação de Dados é altamente eficaz em volumes de até 64 TB.

**O que passou a funcionar de maneira diferente?**
No Windows Server 2012 R2, o pipeline de trabalho da Eliminação de Duplicação de Dados usa um único thread e uma única fila de E/S para cada volume. Para garantir que os trabalhos de otimização não se atrasem, o que causaria a diminuição da taxa geral de economia do volume, grandes conjuntos de dados devem ser divididos em volumes menores. O tamanho do volume apropriado depende de variação esperada para esse volume. Em média, o máximo é de aproximadamente 6 a 7 TB para volumes de alta variação e aproximadamente 9 a 10 TB para volumes de baixa variação.

No Windows Server 2016, o pipeline de trabalho de eliminação de duplicação de dados foi reprojetado para executar vários threads em paralelo usando várias filas de E/S para cada volume. Isso resulta em desempenho que anteriormente só era possível por meio da divisão dos dados em vários volumes menores. Essa alteração é representada na imagem a seguir:

![Uma visualização comparando o pipeline de trabalho de Eliminação de Duplicação de Dados no Windows Server 2012 R2 e no Windows Server 2016](media/server-2016-dedup-job-pipeline.png)

Essas otimizações se aplicam a [todos os trabalhos de Eliminação de Duplicação de Dados](understand.md#job-info), não apenas ao trabalho de Otimização.

## <a name="support-for-large-files"></a><a name="large-file-support"></a>Suporte para arquivos grandes
**Qual é o valor agregado desta alteração?**
No Windows Server 2012 R2, arquivos muito grandes não são bons candidatos para Eliminação de Duplicação de Dados devido à redução do desempenho do pipeline de processamento de Eliminação de Duplicação. No Windows Server 2016, a eliminação de duplicação de arquivos de até 1 TB é muito eficaz, permitindo que os administradores economizem na eliminação de duplicação para um intervalo até maior de cargas de trabalho. Por exemplo, você pode eliminar a duplicação de arquivos muito grandes normalmente associados a cargas de trabalho de backup.

**O que passou a funcionar de maneira diferente?**
No Windows Server 2016, a Eliminação de Duplicação de Dados usa novas estruturas de mapa de fluxo e outros aprimoramentos "de bastidores" para aumentar a produtividade da otimização e o desempenho de acesso. Além disso, o pipeline de processamento da Eliminação de Duplicação pode agora retomar a otimização após um failover em vez de reiniciar. Essas alterações tornam a eliminação de duplicação em arquivos de até 1 TB altamente eficaz.

## <a name="support-for-nano-server"></a><a name="nano-server-support"></a>Suporte ao Nano Server
**Qual é o valor agregado desta alteração?**
O Nano Server é uma nova opção de implantação sem periféricos no Windows Server 2016 que requer uma superfície de recursos de sistema bem menor, inicializa bem mais rapidamente e exige menos atualizações e reinicializações do que a opção de implantação do Windows Server Core. A Eliminação de Duplicação de Dados tem suporte total no Nano Server. Para saber mais sobre o Nano Server, confira [Introdução ao Nano Server](../../get-started/getting-started-with-nano-server.md).

## <a name=""></a><a name="simple-backup-support">Configuração simplificada para aplicativos de backup virtualizados</a>
**Qual é o valor agregado desta alteração?**
A Eliminação de Duplicação de Dados para Aplicativos de Backup Virtualizado é um cenário com suporte no Windows Server 2012 R2, mas ela requer o ajuste manual das configurações de eliminação de duplicação. No Windows Server 2016, a configuração da Eliminação de Duplicação de Dados para Aplicativos de Backup Virtualizado foi drasticamente simplificada. Ela usa uma opção de tipo de uso predefinido ao habilitar a Eliminação de Duplicação para um volume, assim como nossas opções de servidor de arquivos de finalidade geral e VDI.

## <a name=""></a><a name="cluster-upgrade-support">Suporte a atualizações do sistema operacional de cluster sem interrupção</a>
**Qual é o valor agregado desta alteração?**
Clusters de failover do Windows Server que executam a Eliminação de Duplicação de Dados podem ter uma mistura de nós que executam versões de Eliminação de Duplicação de Dados do Windows Server 2012 R2 juntamente com nós que executam versões de Eliminação de Duplicação de Dados do Windows Server 2016. Esse aprimoramento fornece acesso a dados completo a todos os volumes com eliminação de duplicação durante uma atualização de cluster sem interrupção, permitindo a distribuição gradual da nova versão da Eliminação de Duplicação de Dados em um cluster do Windows Server 2012 R2 existente sem incorrer em tempo de inatividade para atualizar todos os nós de uma só vez.

**O que passou a funcionar de maneira diferente?**<br />
Em versões anteriores do Windows Server, um Cluster de Failover do Windows Server exigia que todos os nós do cluster tivessem a mesma versão do Windows Server. A partir do Windows Server 2016, a funcionalidade de atualização sem interrupção permite que um cluster seja executado em modo misto. A Eliminação de Duplicação de Dados dá suporte a essa nova configuração de cluster em modo misto para permitir o acesso a dados completo durante um atualização de cluster sem interrupção.
