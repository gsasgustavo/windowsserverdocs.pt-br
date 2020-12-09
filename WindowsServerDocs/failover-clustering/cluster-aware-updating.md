---
title: Visão geral da Atualização com Suporte a Cluster
description: A atualização de Cluster-Aware (CAU) automatiza a instalação de atualização de software em clusters que executam o Windows Server.
ms.topic: article
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.date: 08/06/2018
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: e729c3e20da1c66581275fb12ec4a5f848475724
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96865735"
---
# <a name="cluster-aware-updating-overview"></a>Visão geral da Atualização com Suporte a Cluster

> Aplica-se a: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Este tópico fornece uma visão geral da \- Cau de atualização com reconhecimento de cluster \( \) , um recurso que automatiza o processo de atualização de software em servidores clusterizados enquanto mantém a disponibilidade.

> [!NOTE]
> Ao atualizar [espaços de armazenamento diretos](../storage/storage-spaces/storage-spaces-direct-overview.md) clusters, recomendamos o uso de Cluster-Aware atualização.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Descrição do recurso
A atualização de Cluster-Aware é um recurso automatizado que permite atualizar servidores em um [cluster de failover](failover-clustering-overview.md) com pouca ou nenhuma perda na disponibilidade durante o processo de atualização. Durante uma execução de atualização, Cluster-Aware atualizando de forma transparente executa as seguintes tarefas:

1. Coloca cada nó do cluster no modo de manutenção do nó.
2. Move as funções clusterizadas para fora do nó.
3. Instala as atualizações e quaisquer atualizações dependentes.
4. Executa uma reinicialização, se necessário.
5. Coloca o nó fora do modo de manutenção.
6. Restaura as funções clusterizadas no nó.
7. Move para atualizar o próximo nó.

Para várias funções clusterizadas no cluster, o processo de atualização automática dispara um failover planejado. Isso pode provocar uma interrupção de serviço transitória nos clientes conectados. No entanto, no caso de cargas de trabalho continuamente disponíveis, como o Hyper- \- V com migração dinâmica ou servidor de arquivos com failover transparente de SMB, a atualização de Cluster-Aware pode coordenar atualizações de cluster sem afetar a disponibilidade do serviço.

## <a name="practical-applications"></a>Aplicações práticas

-   A CAU reduz as interrupções de serviço em serviços clusterizados, reduz a necessidade de soluções alternativas de atualização manual e torna o processo de atualização de cluster de ponta \- a \- ponta mais confiável para o administrador. Quando o recurso CAU é usado em conjunto com cargas de trabalho de cluster disponíveis continuamente, como a carga de trabalho de servidor de arquivos de servidores de arquivos continuamente disponível \( com failover transparente SMB \) ou Hyper \- V, as atualizações de cluster podem ser executadas com impacto zero na disponibilidade do serviço para clientes.

-   A CAU facilita a adoção de processos de TI consistentes em toda a empresa. A atualização de perfis de execução pode ser criada para diferentes classes de clusters de failover e, em seguida, gerenciada centralmente em um compartilhamento de arquivos para garantir que as implantações de CAU em toda a organização de ti apliquem atualizações de forma consistente, mesmo que os clusters sejam gerenciados por diferentes linhas \- de \- negócios ou administradores.

-   A CAU pode agendar as Execuções de Atualização diariamente, semanalmente ou mensalmente para coordenar as atualizações de cluster com outros processos de gerenciamento de TI.

-   A CAU fornece uma arquitetura extensível para atualizar o inventário de software de cluster de \- modo compatível com cluster. Isso pode ser usado por editores para coordenar a instalação de atualizações de software que não são publicadas em Windows Update ou Microsoft Update ou que não estão disponíveis na Microsoft, por exemplo, atualizações para \- drivers de dispositivo não Microsoft.

-   O \- modo de autoatualização da cau permite que um dispositivo "cluster pronto" \( um conjunto de máquinas físicas clusterizadas, normalmente empacotadas em um chassi \) para se atualizar. Normalmente, esses dispositivos são implantados nas filiais locais com suporte mínimo de TI para gerenciar os clusters. O \- modo de autoatualização oferece um ótimo valor nesses cenários de implantação.

## <a name="important-functionality"></a>Funcionalidade importante
Veja a seguir uma descrição da funcionalidade importante de atualização de Cluster-Aware:

-   Uma interface \( do usuário da IU \) -a janela de atualização com reconhecimento de cluster e um conjunto de cmdlets que você pode usar para visualizar, aplicar, monitorar e relatar as atualizações

-   Uma \- \- automação de ponta a ponta da operação de atualização de cluster de \- \( uma execução de atualização \) , orquestrada por um ou mais computadores do coordenador de atualização

-   Um plug \- -in padrão que se integra com o WUA do agente de Windows Update existente \( \) e Windows Server Update Services a \( \) infraestrutura do WSUS no Windows Server para aplicar atualizações importantes da Microsoft

-   Um segundo plug- \- in que pode ser usado para aplicar hotfixes da Microsoft e que pode ser personalizado para aplicar \- atualizações não Microsoft

-   Perfis de Execução de Atualização que você configura com as definições das opções de Execução de Atualização, como o número máximo de vezes que a atualização será repetida por nó. Os Perfis de Execução de Atualização permitem que você reutilize rapidamente as mesmas configurações nas Execuções de Atualização e compartilhe facilmente as configurações de atualização com outros clusters de failover.

-   Uma arquitetura extensível que dá suporte \- a um novo desenvolvimento de plug-in para coordenar outras \- ferramentas de atualização de nó em todo o cluster, como instaladores de software personalizados, ferramentas de atualização de BIOS e adaptador de rede ou adaptador de barramento de host de \( atualização de HBA \) .

A atualização de Cluster-Aware pode coordenar a operação de atualização de cluster completa em dois modos:

-   **\- Modo de autoatualização** para esse modo, a função clusterizada Cau é configurada como uma carga de trabalho no cluster de failover que deve ser atualizada e uma agenda de atualização associada é definida. O cluster se atualiza em horários agendados usando um padrão ou um perfil personalizado para Execução de Atualização. Durante a Execução de Atualização, o processo do Coordenador de Atualização da CAU é iniciado no nó que possui a função clusterizada da CAU e executa as atualizações em cada nó do cluster sequencialmente. Para atualizar o nó do cluster atual, a função clusterizada da CAU faz failover para outro nó do cluster, e um novo processo do Coordenador de Atualização nesse nó assume o controle da Execução de Atualização. No \- modo de autoatualização, a cau pode atualizar o cluster de failover usando um processo de atualização completo e totalmente automatizado \- \- . Um administrador também pode disparar atualizações sob \- demanda nesse modo ou simplesmente usar a abordagem de atualização remota, \- se desejado. No \- modo de autoatualização, um administrador pode obter informações resumidas sobre uma execução de atualização em andamento conectando-se ao cluster e executando o cmdlet **Get \- CauRun** do Windows PowerShell.

-   **O \- modo de atualização remota** para esse modo, um computador remoto, que é chamado de coordenador de atualização, é configurado com as ferramentas de Cau. O Coordenador de Atualização não é um membro do cluster que é atualizado durante a Execução de Atualização. No computador remoto, o administrador dispara uma execução de \- atualização sob demanda usando um perfil de execução de atualização padrão ou personalizado. \-O modo de atualização remota é útil para monitorar \- o andamento em tempo real durante a execução da atualização e para clusters que estão em execução em instalações do Server Core.

## <a name="hardware-and-software-requirements"></a>Requisitos de hardware e software

A CAU pode ser usada em todas as edições do Windows Server, incluindo instalações do Server Core. Para obter informações sobre requisitos detalhados, consulte [requisitos de atualização com suporte a cluster e práticas recomendadas](cluster-aware-updating-requirements.md).

### <a name="installing-cluster-aware-updating"></a>Instalando Cluster-Aware atualizando
Para usar a CAU, instale o recurso de clustering de failover no Windows Server e crie um cluster de failover. Os componentes que suportam a funcionalidade CAU são instalados automaticamente em cada nó do cluster.

Para instalar o recurso Clustering de Failover, você pode usar as seguintes ferramentas:
- Adicionar assistente de funções e recursos no Gerenciador de Servidores
- [Install-WindowsFeature](/powershell/module/servermanager/Install-WindowsFeature?view=winserver2012r2-ps) Cmdlet do Windows PowerShell
- Ferramenta de linha de comando de Gerenciamento e Manutenção de Imagens de Implantação (DISM)

Para obter mais informações, consulte [instalar o recurso de cluster de failover](create-failover-cluster.md#install-the-failover-clustering-feature).

Você também deve instalar as ferramentas de clustering de failover, que fazem parte do Ferramentas de Administração de Servidor Remoto e são instaladas por padrão quando você instala o recurso de clustering de failover no Gerenciador do Servidor. As ferramentas de clustering de failover incluem o Cluster-Aware atualizar a interface do usuário e os cmdlets do PowerShell.

Você deve instalar as Ferramentas de Clustering de Failover da seguinte maneira para dar suporte aos diferentes modos de atualização da CAU:

- Para usar a CAU no \- modo de autoatualização, instale as ferramentas de clustering de failover em cada nó de cluster.

- Para habilitar \- o modo de atualização remota, instale as ferramentas de clustering de failover em um computador que tenha conectividade de rede com o cluster de failover.

> [!NOTE]
> -   Você não pode usar as ferramentas de clustering de failover no Windows Server 2012 para gerenciar Cluster-Aware atualizando em uma versão mais recente do Windows Server.
> -   Para usar a CAU somente no \- modo de atualização remota, a instalação das ferramentas de clustering de failover nos nós do cluster não é necessária. No entanto, alguns recursos da CAU não estarão disponíveis. Para obter mais informações, consulte [requisitos e práticas recomendadas para \- atualização com reconhecimento de cluster](cluster-aware-updating-requirements.md).
> -   A menos que você esteja usando a CAU somente no \- modo de autoatualização, o computador no qual as ferramentas de Cau estão instaladas e que coordena as atualizações não pode ser um membro do cluster de failover.

### <a name="enabling-self-updating-mode"></a>Habilitando o modo de autoatualização
Para habilitar o modo de autoatualização, você deve adicionar a função de cluster Cluster-Aware Atualizando para o cluster de failover. Para fazer isso, use um dos seguintes métodos:
- Em Gerenciador do servidor, selecione **ferramentas**  >  **atualização com suporte a cluster** e, na janela de atualização de Cluster-Aware, selecione **Configurar opções de autoatualização de cluster**.
- Em uma sessão do PowerShell, execute o cmdlet [Add-CauClusterRole](/powershell/module/clusterawareupdating/Add-CauClusterRole) .

Para desinstalar o CAU, desinstale o recurso de clustering de failover ou as ferramentas de clustering de failover usando Gerenciador do Servidor, o cmdlet [Uninstall-WindowsFeature](/powershell/module/servermanager/Uninstall-WindowsFeature) ou as ferramentas de linha de comando do DISM \- .

### <a name="additional-requirements-and-best-practices"></a>Requisitos adicionais e práticas recomendadas

Para que a CAU atualize os nós do cluster com êxito, e para obter mais diretrizes sobre como configurar o ambiente de cluster de failover para usar a CAU, execute o Analisador de Práticas Recomendadas da CAU.

Para obter requisitos detalhados e práticas recomendadas para usar a CAU e informações sobre como executar o Analisador de Práticas Recomendadas CAU, consulte [requisitos e práticas recomendadas para \- atualização com reconhecimento de cluster](cluster-aware-updating-requirements.md).

### <a name="starting-cluster-aware-updating"></a>Iniciando atualização de Cluster-Aware

##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>Para iniciar a atualização de Cluster-Aware do Gerenciador do Servidor

1.  Inicie o Gerenciador do Servidor.

2.  Realize uma destas ações:

    -   No menu **ferramentas** , clique em **\- atualização com reconhecimento de cluster**.

    -   Se um ou mais nós de cluster, ou o cluster, for adicionado ao Gerenciador do Servidor, na página **todos os servidores** , \- clique com o botão direito do mouse no nome de um nó \( ou no nome do cluster \) e clique em **Atualizar cluster**.

## <a name="additional-references"></a>Referências adicionais
Os links a seguir fornecem mais informações sobre como usar a atualização de Cluster-Aware.

-   [Requisitos e práticas recomendadas para \- atualização com reconhecimento de cluster](cluster-aware-updating.md)

-   [\-Atualização com reconhecimento de cluster: perguntas frequentes](cluster-aware-updating-faq.md)

-   [Opções avançadas e perfis de execução de atualização da CAU](cluster-aware-updating-options.md)

-   [Como funcionam os plug-ins da CAU \-](cluster-aware-updating-plug-ins.md)

-   [\-Cmdlets de atualização com reconhecimento de cluster no Windows PowerShell](/powershell/module/clusterawareupdating/)

-   [\-Referência de plug- \- in de atualização com reconhecimento de cluster](/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)
