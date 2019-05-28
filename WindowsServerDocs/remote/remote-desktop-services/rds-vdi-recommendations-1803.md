---
title: Otimizando o Windows 10, versão 1803, para uma função Virtual Desktop Infrastructure (VDI)
description: Recomendado as configurações e definições para minimizar a sobrecarga para o Windows 10 1803) usadas como imagens VDI de áreas de trabalho
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: robsmi
ms.suite: na
ms.technology: remote-desktop-services
ms.author: jaimeo, robsmi
ms.tgt_pltfrm: na
ms.topic: article
author: jaimeo
manager: dougkim
ms.openlocfilehash: 2af0ea64ce88431bfb6a4922ae7a471862ed7f82
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034636"
---
# <a name="optimizing-windows-10-version-1803-for-a-virtual-desktop-infrastructure-vdi-role"></a>Otimizando o Windows 10, versão 1803, para uma função Virtual Desktop Infrastructure (VDI)

Este artigo ajuda você a escolher as configurações para Windows 10, versão 1803 (build 17134) que deve resultar em melhor desempenho em um ambiente virtualizado Desktop Infrastructure (VDI). Todas as configurações neste guia estão *recomendações a serem considerados* e estão em nenhum requisito de forma.

Em um ambiente de VDI principais maneiras de otimizar o desempenho do Windows 10 são minimizar o aplicativo gráfico redesenha atividades em segundo plano que não geram nenhum benefício principal para o ambiente de VDI, e geralmente reduzir processos em execução para o mínimo necessário. Das metas secundárias é reduzir o uso de espaço em disco na imagem de base para o mínimo necessário. Com o VDI implementações, o menor possível base de dados de ou tamanho da imagem "gold", pode reduzir um pouco uso de memória no hipervisor, bem como uma pequena redução em operações de rede geral necessária para fornecer a imagem da área de trabalho para o consumidor.

> [!NOTE]  
> Configurações recomendadas aqui podem ser aplicadas para outra instalação do Windows 10, versão 1803, incluindo aqueles em físicos ou outros dispositivos virtuais. Não há recomendações neste tópico devem afetar a capacidade de suporte do Windows 10, versão 1803.

> [!TIP]  
> Um script que implementa as otimizações discutidas neste tópico, bem como um arquivo de exportação de GPO que você pode importar com **LGPO.exe**– está disponível em [TheVDIGuys](https://github.com//TheVDIGuys) no GitHub.

## <a name="vdi-optimization-principles"></a>Princípios de otimização do VDI

Um ambiente de VDI apresenta uma sessão de área de trabalho completa, incluindo aplicativos, para um usuário de computador em uma rede. Ambientes de VDI geralmente usam uma imagem de sistema operacional base, que, em seguida, torna-se a base para as áreas de trabalho subsequentemente apresentada aos usuários para o trabalho. Há variações das implementações do VDI, como "persistentes", "não persistentes" e "sessão da área de trabalho". O tipo persistente preserva as alterações para o sistema operacional da área de trabalho VDI de uma sessão para o próximo. O tipo não persistentes não preserva as alterações para o sistema operacional da área de trabalho VDI de uma sessão para o próximo. Para o usuário essa área de trabalho é pouco diferente de outro dispositivo físico ou virtual, além de que ele é acessado através de uma rede.

As configurações de otimização podem ocorrer em um dispositivo de referência. Uma VM é um lugar ideal para montar a imagem, porque você pode salvar o estado, verifique os pontos de verificação e os backups podem ser feitos e outras tarefas úteis. Comece instalando o sistema operacional padrão na VM base e, em seguida, otimize a VM de base para o uso VDI removendo aplicativos desnecessários, instalação de atualizações do Windows, instalar outras atualizações, excluindo arquivos temporários, aplicação de configurações, etc.

Há outros tipos de VDI, como serviços da área de trabalho persistentes e remotos (RDS). Uma discussão detalhada sobre essas tecnologias está fora do escopo deste tópico, configurações de imagem com referência a outros fatores no ambiente, como a otimização de host de base do qual o Windows se concentra.

### <a name="persistent-vdi"></a>VDI persistente

No nível básico, persistente VDI é uma VM que salva o estado do sistema operacional entre reinicializações. Outras camadas de software da solução VDI fornecem o acesso fácil e direta de usuários a suas máquinas virtuais atribuídos, geralmente com uma única solução de logon.

Há várias implementações diferentes de VDI persistente:

-   Máquinas virtuais tradicionais, em que a VM tem seu próprio arquivo de disco virtual, é iniciado normalmente, salva as alterações de uma sessão para o próximo e é essencialmente uma VM normal. A diferença é como o usuário acessa essa VM. Pode haver um portal da web que o usuário faz login que automaticamente direciona o usuário para seu um ou mais atribuído a máquinas virtuais de VDI.

-   Baseia a imagem de máquina virtual persistente, com discos virtuais pessoais. Nesse tipo de implementação, há uma imagem de base/ouro em um ou mais servidores de host. Uma VM é criada, e um ou mais discos virtuais são criados e atribuídos a esse disco para armazenamento persistente.

    -   Quando a VM é iniciada, uma cópia da imagem base é lido na memória da VM. Ao mesmo tempo, um disco virtual persistente, atribuído a essa VM, com as alterações do sistema operacional anterior mesclado por meio de um processo complexo.

    -   As alterações, como gravações de log de eventos, gravações de log, etc. são redirecionadas para o disco virtual de leitura/gravação atribuído a essa VM.

    -   Nessa circunstância, sistema operacional e a manutenção do aplicativo podem operar normalmente, usando o software de manutenção tradicionais, como o Windows Server Update Services ou outras tecnologias de gerenciamento.

### <a name="non-persistent-vdi"></a>VDI não persistente

Quando uma implementação de VDI não persistente é baseada em uma base ou a imagem "ouro", as otimizações são executadas principalmente, na imagem de base e, em seguida, por meio de diretivas locais e as configurações locais.

Com o VDI não persistente baseada em imagem, a imagem base é somente leitura. Quando uma VM de VDI não persistente é iniciada, uma cópia da imagem base é transmitida para a máquina virtual. Atividade que ocorre durante a inicialização e daí em diante, até a próxima reinicialização é redirecionada para um local temporário. Normalmente, os usuários são fornecidos locais de rede para armazenar seus dados. Em alguns casos, o perfil do usuário é mesclado com o VM padrão para fornecer ao usuário suas configurações.

Manutenção de um aspecto importante da VDI não persitent que se baseia em uma única imagem. Atualizações para o sistema operacional são entregues, geralmente, uma vez por mês.
Com o VDI baseada em imagem, há um conjunto de processos para executar a fim de obter atualizações para a imagem:

-   Em um determinado host, todas as VMs no host que são derivados da imagem base deve ser desligado ou desativado. Isso significa que os usuários são redirecionados para outras VMs.

-   A imagem base, em seguida, é aberta e iniciada. Todas as atividades de manutenção, em seguida, são executadas, como atualizações do sistema operacional, atualizações do .NET, as atualizações de aplicativo, etc.

-   Todas as novas configurações que precisam ser aplicadas são aplicadas no momento.

-   Qualquer outra manutenção é executada no momento.

-   A imagem base, em seguida, é desligada.

-   A imagem base é selada e definida para voltar para a produção.

-   Os usuários têm permissão para fazer logon novamente.

> [!NOTE]  
> Windows 10 executa um conjunto de tarefas de manutenção automaticamente, em intervalos periódicos. Há uma tarefa agendada que é definida para ser executado às 3:00, horário local em todos os dias por padrão. Esta tarefa agendada executa uma lista de tarefas, incluindo a limpeza do Windows Update. Você pode exibir todas as categorias de manutenção que ocorrem automaticamente com este comando do PowerShell:

`Get-ScheduledTask | ? {$_.Settings.MaintenanceSettings}`



Um dos desafios com o VDI não persistente é que, quando um usuário fizer logoff, quase todas as atividades de sistema operacional é descartada. Do usuário perfil e ou estado pode ser salvo, mas a própria máquina virtual descarta quase todas as alterações que foram feitas desde a última inicialização. Portanto, destinadas a um computador Windows que salva o estado de uma sessão para o próximo de otimizações não são aplicáveis.

Dependendo da arquitetura de VM de VDI, reinicie o coisas like pré-busca e SuperFetch são não vai ajudar de uma sessão para o próximo, como todas as otimizações são descartadas na VM. A indexação pode ser uma perda parcial de recursos, como seriam qualquer otimizações de disco como uma desfragmentação tradicional.

### <a name="to-sysprep-or-not-sysprep"></a>Sysprep ou não o Sysprep

Windows 10 tem uma funcionalidade interna chamada a [ferramenta de preparação do sistema](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview), (geralmente abbreviiated "Sysprep"). A ferramenta Sysprep é usada para preparar uma imagem personalizada do Windows 10 para duplicação. O processo Sysprep garante que o sistema operacional resultante é corretamente exclusivo para executar em produção.

Há motivos para e contra a execução de Sysprep. No caso de VDI, convém a capacidade de personalizar o perfil de usuário padrão que será usado como o modelo de perfil para os próximos usuários que fizerem logon usando essa imagem. Você pode ter aplicativos que você deseja instalado, mas também pode controlar as configurações por aplicativo.

A alternativa é usar um padrão. ISO para instalar, possivelmente usando um arquivo de resposta de instalação autônoma e uma sequência de tarefas para instalar aplicativos ou remover aplicativos. Você também pode usar uma sequência de tarefas para definir configurações de política local na imagem, talvez usando o [Local grupo de política de objeto utilitário (LGPO)](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) ferramenta.

#### <a name="vdi-optimization-categories"></a>Categorias de otimização do VDI


-   Configurações do sistema operacional global

    -   Limpeza de aplicativo UWP

    -   Limpeza de recursos opcional

    -   Configurações de política local

    -   Serviços do sistema

    -   Tarefas Agendadas

    -   Aplicar atualizações do Windows

    -   Rastreamentos automática do Windows

    -   Limpeza de disco antes da imagem finalizando (lacre)

-   Configurações do usuário

-   Hipervisor / configurações de Host

##### <a name="global-vdi-operating-system-optimization"></a>Otimização global de sistema operacional VDI

Configurações globais do VDI incluem o seguinte:

-   [Limpeza de aplicativo universal Windows Platform (UWP)](#universal-windows-platform-app-cleanup)

-   [Limpar recursos opcionais](#clean-up-optional-features)

-   [Configurações de diretiva local](#local-policy-settings)

-   [Serviços do sistema](#system-services)

-   [Tarefas agendadas](#scheduled-tasks)

-   [Aplicar o Windows e outras atualizações](#apply-windows-and-other-updates)

-   [Rastreamentos automática do Windows](#automatic-windows-traces)

-   [Otimização do Windows Defender com VDI](#windows-defender-optimization-with-vdi)

-   [Ajustando o desempenho de rede do Windows 10 usando as configurações do registro](#tuning-windows-10-network-performance-by-using-registry-settings)

-   Configurações adicionais do [Windows restrito tráfego limitado funcionalidade de linha de base](https://go.microsoft.com/fwlink/?linkid=828887) diretrizes.

-   [Limpeza de disco](#disk-cleanup-including-using-the-disk-cleanup-wizard)

### <a name="universal-windows-platform-app-cleanup"></a>Limpeza de aplicativo de plataforma Windows universal

Uma das metas de uma imagem de VDI é ser tão pequeno quanto possível. Uma maneira de reduzir o tamanho da imagem é remover aplicativos da UWP que não serão usados no ambiente. Com aplicativos UWP, há os arquivos de aplicativo principal, também conhecido como a carga. Há uma pequena quantidade de dados armazenados em cada perfil de usuário para configurações específicas do aplicativo. Também há uma pequena quantidade de dados no perfil todos os usuários.

Conectividade e o intervalo são tudo o que diz respeito à limpeza de aplicativo UWP. Se você implantar sua imagem de base para um dispositivo sem conectividade de rede, Windows 10 não é possível conectar-se para a Microsoft Store e baixar aplicativos e tente instalá-los enquanto você está tentando desinstalá-los.

Se você modificar sua base. Desnecessários de WIM que você usa para instalar o Windows 10 e remover aplicativos UWP da. WIM antes de instalar, os aplicativos não serão instalados para começar e seus tempos de criação de perfil devem ser menores. Mais adiante nesta seção, você encontrará informações sobre como remover aplicativos da UWP da instalação. Arquivo WIM.

É uma boa estratégia para VDI provisionar os aplicativos que você deseja na imagem de base, em seguida, limitar ou bloquear o acesso para a Microsoft Store posteriormente. Aplicativos da Store são atualizados periodicamente em segundo plano em computadores normais. Os aplicativos UWP podem ser atualizados durante a janela de manutenção quando outras atualizações são aplicadas. 

#### <a name="delete-the-payload-of-uwp-apps"></a>Excluir o conteúdo de aplicativos UWP

Aplicativos UWP que não são necessários ainda estão em sistema de arquivos que consome uma quantidade pequena de espaço em disco. Para aplicativos que nunca serão necessários, a carga de aplicativos da UWP indesejados pode ser removida da imagem base usando comandos do PowerShell.

Na verdade, se você remover aqueles da instalação. Arquivo WIM usando os links fornecidos posteriormente nesta seção, você poderá começar do zero com uma lista muito pequena de aplicativos UWP.

Execute o seguinte comando para enumerar os aplicativos da UWP provisionados de um sistema de operacional Windows 10 em execução, como nessa saída truncada do exemplo do PowerShell:

```powershell

    Get-AppxProvisionedPackage -Online 
    
    DisplayName  : Microsoft.3DBuilder
    Version      : 13.0.10349.0  
    Architecture : neutral
    ResourceId   : \~ 
    PackageName  : Microsoft.3DBuilder_13.0.10349.0_neutral_\~_8wekyb3d8bbwe 
    Regions      : 
    ...
```


Aplicativos da UWP que são provisionados para um sistema podem ser removidos durante a instalação do sistema operacional como parte de uma sequência de tarefas, ou posterior depois que o sistema operacional está instalado. Isso pode ser o método preferencial, pois ele torna o processo geral de criação ou manutenção de uma imagem modular. Depois de desenvolver os scripts, se algo for alterado em um build posterior editar um script existente em vez de repetir o processo do zero. Aqui estão alguns links para informações sobre este tópico:

[Removendo aplicativos nativos do Windows 10 durante uma sequência de tarefas](https://blogs.technet.microsoft.com/mniehaus/2015/11/11/removing-windows-10-in-box-apps-during-a-task-sequence/)

[Removendo aplicativos internos do Windows 10-arquivo WIM com o Powershell - versão 1.3](https://gallery.technet.microsoft.com/Removing-Built-in-apps-65dc387b)

[Windows 10 1607: Mantendo os aplicativos de entrada ao implantar a atualização de recurso](https://blogs.technet.microsoft.com/mniehaus/2016/08/23/windows-10-1607-keeping-apps-from-coming-back-when-deploying-the-feature-update/)

Em seguida, execute as [AppxProvisionedPackage remover](https://docs.microsoft.com/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) comando do PowerShell para remover as cargas de aplicativo UWP:

`Remove-AppxProvisionedPackage -Online -PackageName MyAppxPackage`

Cada aplicativo UWP deve ser avaliado para aplicabilidade de cada ambiente exclusivo. Você desejará fazer uma instalação padrão do Windows 10, versão 1803, em seguida, observe quais aplicativos estão em execução e consumindo memória. Por exemplo, você talvez queira considerar a remoção de aplicativos que são iniciados automaticamente, ou aplicativos que automaticamente exibem informações no menu Iniciar, como o clima e notícias, e que não podem ser úteis em seu ambiente.

Um dos aplicativos de UWP de "caixa de entrada" chamados fotos, tem uma configuração chamada padrão **mostrará uma notificação quando novos álbuns estão disponíveis**.  O aplicativo de fotos pode usar aproximadamente 145 MB de memória; conjunto de trabalho privado especificamente memória, até mesma se não está sendo usado.  Alterando a **mostrará uma notificação quando novos álbuns estão disponíveis** configuração para todos os usuários não é prático em esse tempo, portanto, a recomendação para remover o aplicativo de fotos, se ele não é necessário ou desejado.

### <a name="clean-up-optional-features"></a>Limpar recursos opcionais

#### <a name="managing-optional-features-with-powershell"></a>Gerenciamento de recursos opcionais com o PowerShell

 Para enumerar os recursos do Windows instalada no momento, execute este comando do PowerShell:

`Get-WindowsOptionalFeature -Online`


Você pode habilitar ou desabilitar um recurso opcional do Windows específico, como neste exemplo:

`Enable-WindowsOptionalFeature -Online -FeatureName "DirectPlay" -All`

Para obter mais informações sobre isso, consulte [Windows 10: Gerenciamento de recursos opcionais com o PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/39386.windows-10-managing-optional-features-with-powershell.aspx).

#### <a name="enable-or-disable-windows-features-by-using-dism"></a>Ativar ou desativar recursos do Windows usando o DISM

Você pode usar o interno **Dism.exe** ferramenta para enumerar e controlar os recursos opcionais do Windows. Você pode configurar um script Dism.exe para executar durante uma sequência de tarefas que instala o sistema operacional.

### <a name="local-policy-settings"></a>Configurações de política local

Muitas otimizações para Windows 10 em um ambiente de VDI podem ser feitas usando a política do Windows. As configurações listadas aqui podem ser aplicadas localmente à imagem base. Em seguida, se as configurações equivalentes não forem especificadas em qualquer outra forma, como pela diretiva de grupo, as configurações ainda seriam aplicada.

Algumas decisões podem ser baseadas nas especificações do ambiente, por exemplo:

-   O ambiente de VDI tem permissão para acessar a Internet?

-   É a solução VDI não persistente ou persistente?

As configurações a seguir especificamente não contador ou entrar em conflito com qualquer configuração que tem algo a ver com segurança. Essas configurações foram escolhidas para remover as configurações que podem não ser aplicáveis para ambientes de VDI.

> [!NOTE]  
> Nesta tabela de configurações de diretiva de grupo, os itens marcados com um asterisco são do [Windows restrito tráfego limitado funcionalidade de linha de base](https://go.microsoft.com/fwlink/?linkid=828887).

| Configuração de política   | Item    | Subitem     | Configuração possível e comentários   |
|------------------|---------|--------------|--------|
| **Política do computador local \\ configuração do computador \\ configurações do Windows \\ as configurações de segurança**  | |  |        |
| **Políticas do Gerenciador de listas de rede**                   | Todas as propriedades de redes                   | Local de rede     | Usuário não pode alterar o local                                                                                                                                   |
| **Política do computador local \\ configuração do computador \\ modelos administrativos \\ painel de controle**                    |                                           |                      |                                                                                                                                                                               |
| \***Painel de controle**                                 | Permitir dicas Online                                         |                      | Desabilitado (as configurações serão não entre em contato com os serviços de conteúdo da Microsoft para recuperar as dicas e conteúdo da Ajuda)                                                                                                                                                             |
| **\*Painel de controle** \\ personalização                               | Não exibir a tela de bloqueio                            |                      | Habilitado (essa configuração de política controla se a tela de bloqueio é exibida para os usuários. Se você habilitar essa configuração de política, os usuários que não seja necessário pressionar CTRL + ALT + DEL antes de entrar no verão seu bloco selecionado após bloquear seus PCs.)                                                                                                                             |
| **\*Painel de controle** \\ personalização                               | Forçar uma imagem de logon e tela de bloqueio padrão específicos                      |[![Imagem da interface do usuário para definir o caminho para a imagem de tela de bloqueio](media/lock-screen-image-settings.png)](media/lock-screen-image-settings.png)             | Habilitado (essa configuração permite que você especifique a tela de bloqueio padrão e a imagem de logon mostrada quando nenhum usuário está conectado em objetos e também define a imagem especificada como o padrão para todos os usuários, ele substitui a imagem padrão.) Uma baixa resolução, imagem de não-complexos faria com que menos dados transmitidos pela rede a cada vez que a imagem é renderizada.                                                                                                       |
| **\*Painel de controle** \\ opções regionais e idiomas\\personalização de manuscrito                    | Desativar o aprendizado automático                               |                      | Ativado (se você habilitar essa configuração de diretiva, paradas do aprendizado automático, e todos os dados armazenados são excluídos. Os usuários não é possível definir essa configuração no painel de controle)                                                                                                                                                   |
| **Política do computador local \\ configuração do computador \\ modelos administrativos \\ rede**          |                                           |                      |                                                                                                                                                                               |
| **Serviço de transferência inteligente em segundo plano (BITS)**                                  | Não permitir que o cliente de BITS usar o Cache de ramificação do Windows                                  |                      | Enabled                                                                                                                                                                                       |
| **Serviço de transferência inteligente em segundo plano (BITS)**                                  | Não permitir que o computador atuar como um cliente de cache par do BITS                             |                      | Enabled                                                                                                                                                                                       |
| **Serviço de transferência inteligente em segundo plano (BITS)**                                  | Não permitir que o computador atuar como um servidor de cache par do BITS                             |                      | Enabled                                                                                                                                                                                       |
| **Serviço de transferência inteligente em segundo plano (BITS)**                                  | Permitir que o cache par do BITS                                    |                      | Desabilitada                                                                                                                                                                                      |
| **BranchCache**                                     | Ativar o BranchCache                                       |                      | Desabilitada                                                                                                                                                                                      |
| \***Fontes**                                         | Permitir que os provedores de fonte                                     |                      | Desabilitado (o Windows não se conecta a um provedor de fontes online e enumera apenas as fontes instaladas localmente.)                                                                                                                                                    |
| **Autenticação de ponto de acesso**                          | Habilitar a autenticação de ponto de acesso                             |                      | Desabilitada                                                                                                                                                                                      |
| **Serviços de rede ponto a ponto da Microsoft**                      | Desativar os serviços de rede ponto a ponto da Microsoft                       |                      | Enabled                                                                                                                                                                                       |
| **Indicador de Status de conectividade de rede** (Observe que há outras configurações nesta seção que pode ser usado em redes isoladas)                           | Especificar polling passivo                                   | Desabilitar polling passivo (caixa de seleção)                   | Ativado (Use essa configuração se uma rede isolada,) ou usando endereços IP estáticos                                                                                                                                                            |
| **Arquivos offline**                                   | Permitir ou não permitir usar o recurso Arquivos Offline                        |                      | Desabilitada                                                                                                                                                                                      |
| **\*Configurações de TCPIP** \\ tecnologias de transição IPv6                                 | Definir estado de Teredo                                          | Estado desabilitado                       | Habilitado (no estado desabilitado nenhuma interface Teredo está presente no host.)                                                                                                                                                                       |
| **\*Serviço WLAN** \\ configurações de rede local sem fio                                  | Permitir que o Windows se conecte automaticamente a hotspots abertos sugeridas, compartilhados por contatos de redes e pontos de acesso oferecendo serviços pagos |                      | Desabilitado (**conectar a hotspots abertos sugeridos**, **conectar a redes compartilhadas por Meus contatos**, e **habilitar os serviços pagos** será desativado e os usuários sobre este dispositivo será ser impedido de habilitá-los.)                                                                                                                                |
| **Política do computador local \\ configuração do computador \\ modelos administrativos \\ Menu Iniciar e barra de tarefas**           |                                           |                      |                                                                                                                                                                               |
| \***Notificações**                                 | Desativar o uso de rede de notificações                                      |                      | Ativado (se você habilitar essa configuração de política, aplicativos e recursos do sistema não será capazes de receber notificações de rede de WNS ou por meio de APIs de sondagem de notificação).                                                                                                                                               |
| **Política do computador local \\ configuração do computador \\ modelos administrativos \\ sistema**           |                                           |                      |                                                                                                                                                                               |
| **Instalação de dispositivo**                             | Não enviar um relatório de erros do Windows quando um driver genérico é instalado em um dispositivo                         |                      | Enabled                                                                                                                                                                                       |
| **Instalação de dispositivo**                             | Impedir a criação de um ponto de restauração do sistema durante a atividade de dispositivo que normalmente seria solicitam a criação de um ponto de restauração                  |                      | Enabled                                                                                                                                                                                       |
| **Instalação de dispositivo**                             | Impedir a recuperação de metadados de dispositivo da Internet                       |                      | Enabled                                                                                                                                                                                       |
| **Instalação de dispositivo**                             | Impedir a enviar um relatório de erro quando um solicitações adicionais de software durante a instalação do Windows        |                      | Enabled                                                                                                                                                                                       |
| **Instalação de dispositivo**                             | Desative **adicionar novo Hardware** balões durante a instalação do dispositivo                         |                      | Enabled                                                                                                                                                                                       |
| **Sistema de arquivos**\\NTFS                                | Opções de criação de nome curto                               | Desabilitado em todos os volumes              | Enabled                                                                                                                                                                                       |
| \***Política de grupo**                                  | Configurar o aplicativo de web vinculação com manipuladores de URL do aplicativo                        |                      | Desabilitado (desabilita vinculação de aplicativo web e HTTP (s) URIs serão aberto no navegador padrão, em vez de starging o aplicativo associado.)                                                                                                                                                         |
| \***Política de grupo**                                  | Continuar experiências neste dispositivo                                       |                      | Desabilitado (o dispositivo Windows não é detectável por outros dispositivos e não pode participar de experiências entre dispositivos.)                                                                                                                                                         |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar o acesso a todos os recursos do Windows Update                            |                      | Ativado (se você habilitar essa configuração de política, a atualização do Windows todos os recursos são removidos. Isso inclui o bloqueio de acesso para o site Windows Update em http://windowsupdate.microsoft.com, pelo hiperlink Windows Update no menu Iniciar e também no menu Ferramentas no Internet Explorer. A atualização automática do Windows também é desabilitada; Você não será notificado sobre nem receberá atualizações críticas do Windows Update. Essa configuração de política também impede que o Gerenciador de dispositivos instale automaticamente atualizações de driver do site Windows Update.)                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar a atualização automática de certificados de raiz                               |                      | Habilitado (se você habilitar essa configuração de política, quando você é apresentados com um certificado emitido por uma autoridade raiz não confiável, o computador não contatar o site do Windows Update para verificar se a Microsoft adicionou a autoridade de certificação à sua lista de autoridades confiáveis.)    **OBSERVAÇÃO:** Só use essa política se você tiver um meio alternativo para a lista de revogação de certificado mais recente.                                                                                                           |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar links "Events. asp" do Visualizador de eventos                                  |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar compartilhamento de dados de personalização de manuscrito                         |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar relatório de erros de reconhecimento de manuscrito                          |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar Centro de Ajuda e suporte "Você sabia?" content                                  |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desabilitar pesquisa na Ajuda e suporte Center Microsoft Knowledge Base                          |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar Assistente de Conexão de Internet se a conexão de URL fizer referência a Microsoft.com                       |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar download na Internet para publicação na Web e assistentes de pedidos online                 |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar o serviço de associação de arquivo da Internet                                |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar registro se a conexão de URL fizer referência a Microsoft.com                     |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar a tarefa de imagem "Encomendar cópias"                                  |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar a tarefa "Publicar na Web" para arquivos e pastas                                  |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar o programa de Aperfeiçoamento da experiência do Windows Messenger cliente                    |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar o programa de Aperfeiçoamento da experiência do usuário do Windows                                  |                      | Enabled                                                                                                                                                                                       |
| **\*Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                           | Desativar testes ativos do indicador de Status de conectividade de rede do Windows                       |                      | Habilitado (essa configuração de política desativa os testes ativos executados pelo Windows rede conectividade Status NCSI (indicador) para determinar se o computador está conectado à Internet ou a uma rede mais limitada como parte da determinação do nível de conectividade, NCSI executa um dos dois testes ativos: download de uma página de um servidor Web dedicado ou fazer uma solicitação DNS para um endereço dedicado. Se você habilitar essa configuração de política, NCSI não executa qualquer um dos dois testes de Active Directory. Isso pode reduzir a capacidade de NCSI e de outros componentes que usam NCSI, para determinar o acesso à Internet) Observação: Há outras políticas que permitem que você redirecione NCSI testes para recursos internos, se desejar essa funcionalidade. |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar relatório de erros do Windows                          |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento da comunicação da Internet** \\ configurações de comunicação da Internet                             | Desativar a pesquisa de driver de dispositivo do Windows Update                           |                      | Enabled                                                                                                                                                                                       |
| **Logon**                                           | Mostrar primeira animação de assinatura                              |                      | Desabilitada                                                                                                                                                                                      |
| **Logon**                                           | Desativar notificações de aplicativos na tela de bloqueio                             |                      | Enabled                                                                                                                                                                                       |
| **Logon**                                           | Desativar a inicialização do Windows som                            |                      | Enabled                                                                                                                                                                                       |
| **Gerenciamento de energia**                                | Selecione um plano de energia ativo                               | Alto desempenho                     | Enabled                                                                                                                                                                                       |
| **Recuperação**                                        | Permitir a restauração do sistema para o estado padrão                                  |                      | Desabilitada                                                                                                                                                                                      |
| \***Integridade do armazenamento**                                | Permitir download de atualizações para o modelo de previsão de falha de disco                            |                      | Desabilitado (atualizações não seriam baixadas para o modelo de falha de previsão de falha de disco)                                                                                                                                                      |
| \***Serviços de tempo do Windows** \\ provedores de tempo                        | Habilitar cliente do Windows NTP                                 |                      | Desabilitado (se você desabilitar ou não definir essa configuração de política, o relógio do computador local não sincroniza tempo com os servidores NTP) **Observação**: *Considere essa configuração com muito cuidado*. Dispositivos Windows que ingressaram em um domínio devem usar **NT5DS**. Controlador de domínio para o domínio pai DC pode usar o NTP. Função PDCe pode usar o NTP. Às vezes, as máquinas virtuais usam "aprimoramentos" ou "integration services".                                                                                       |
| **Solução de problemas e diagnóstico** \\ manutenção agendada                         | Configurar o comportamento de manutenção agendada                                  |                      | Desabilitada                                                                                                                                                                                      |
| **Solução de problemas e diagnóstico** \\ diagnóstico de desempenho de inicialização do Windows                          | Configurar o nível de execução do cenário                                        |                      | Desabilitada                                                                                                                                                                                      |
| **Solução de problemas e diagnóstico** \\ diagnóstico de vazamento de memória do Windows               | Configurar o nível de execução do cenário                                        |                      | Desabilitada                                                                                                                                                                                      |
| **Solução de problemas e diagnóstico** \\ detecção de esgotamento de recursos do Windows e resolução          | Configurar o nível de execução do cenário                                        |                      | Desabilitada                                                                                                                                                                                      |
| **Solução de problemas e diagnóstico** \\ diagnóstico de desempenho de desligamento do Windows                      | Configurar o nível de execução do cenário                                        |                      | Desabilitada                                                                                                                                                                                      |
| **Solução de problemas e diagnóstico** \\ diagnóstico de desempenho do Windows em espera/retomar                | Configurar o nível de execução do cenário                                        |                      | Desabilitada                                                                                                                                                                                      |
| **Solução de problemas e diagnóstico** \\ diagnóstico de desempenho de capacidade de resposta de sistema do Windows                         | Configurar o nível de execução do cenário                                        |                      | Desabilitada                                                                                                                                                                                      |
| \***Perfis de usuário**                                 | Desligar a ID de anúncio                               |                      | Ativado (se você habilitar essa configuração de política, o anúncio ID está desativado. Aplicativos não é possível usar a ID para experiências entre aplicativos.)                                                                                                                                              |
| **Política do computador local \\ configuração do computador \\ modelos administrativos \\ componentes do Windows**               |                                           |                      |                                                                                                                                                                               |
| **Adicionar recursos ao Windows 10**                                      | Impedir que o assistente seja executado                           |                      | Enabled                                                                                                                                                                                       |
| \***Privacidade do aplicativo**                                   | Let Windows apps access account information                               | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar informações de conta e funcionários da sua organização não é possível alterá-la)                                                                                                                                               |
| \***Privacidade do aplicativo**                                   | Let histórico de chamadas de acesso para aplicativos Windows                                      | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar o histórico de chamadas e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                                  |
| \***Privacidade do aplicativo**                                   | Let Windows apps access contacts                          | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar os contatos e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                         |
| \***Privacidade do aplicativo**                                   | Permitir que os aplicativos do Windows acessem informações de diagnóstico sobre outros aplicativos                           | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você desabilitar ou não definir essa configuração de política, os funcionários da sua organização podem decidir se os aplicativos do Windows podem obter informações de diagnóstico sobre outros aplicativos, usando as configurações \> privacidade no dispositivo)                                                                                                                                   |
| \***Privacidade do aplicativo**                                   | Permitir que o email de acesso de aplicativos do Windows                             | Padrão para todos os aplicativos: Forçar negar                     | Ativado (se você escolher a opção "Permitir força", aplicativos do Windows têm permissão para acessar o email e funcionários da sua organização não é possível alterá-la)                                                                                                                                                |
| \***Privacidade do aplicativo**                                   | Permitir que aplicativos do Windows acessem a localização                          | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar o local e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                         |
| \***Privacidade do aplicativo**                                   | Let Windows apps access messaging                         | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar o local e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                          |
| \***Privacidade do aplicativo**                                   | Permitir que o movimento de acesso de aplicativos do Windows                            | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar dados de movimento e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                                      |
| \***Privacidade do aplicativo**                                   | Permitir que as notificações de acesso de aplicativos do Windows                                     | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar as notificações e funcionários da sua organização não é possível alterá-la)                                                                                                                                                     |
| \***Privacidade do aplicativo**                                   | Permitir que o Windows as tarefas de acesso de aplicativos                             | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar as tarefas e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                            |
| \***Privacidade do aplicativo**                                   | Let Windows apps access the calendar                                      | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar o calendário e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                                      |
| \***Privacidade do aplicativo**                                   | Permitir que aplicativos do Windows acessem a câmera                                        | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar a câmera e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                        |
| \***Privacidade do aplicativo**                                   | Let Windows apps access the microphone                                    | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar o microfone e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                                    |
| \***Privacidade do aplicativo**                                   | Let Windows apps access trusted devices                                   | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para acessar os dispositivos confiáveis e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                                   |
| \***Privacidade do aplicativo**                                   | Permitir que os aplicativos se comunicar com dispositivos não emparelhados do Windows                        | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não têm permissão para se comunicar com dispositivos sem fio não emparelhados e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                               |
| \***Privacidade do aplicativo**                                   | Permitir que os rádios de acesso de aplicativos do Windows                            | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não terá acesso ao controle rádios e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                                      |
| **Privacidade do aplicativo**                                     | Permitir que os aplicativos do Windows fazer chamadas telefônicas                         | Padrão para todos os aplicativos: Forçar negar                     | Ativado (aplicativos do Windows não têm permissão para fazer chamadas telefônicas e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                                                |
| \***Privacidade do aplicativo**                                   | Permitir que os aplicativos executados em segundo plano do Windows                                    | Padrão para todos os aplicativos: Forçar negar                     | Habilitado (se você escolher o **Force negar** opção, aplicativos do Windows não podem ser executados em segundo plano e funcionários da sua organização não é possível alterá-lo.)                                                                                                                                                    |
| **Políticas de reprodução automática**                               | Definir o comportamento padrão para a execução automática                                      | Não execute os comandos de execução automática                  | Enabled                                                                                                                                                                                       |
| \***Políticas de reprodução automática**                             | Desativar a reprodução automática                                         |                      | Habilitado (se você habilitar essa configuração de política, reprodução automática é desabilitado em CD-ROM e unidades de mídia removível ou desabilitado em todas as unidades.)                                                                                                                                             |
| \***Conteúdo de nuvem**                                 | Não Mostrar dicas do Windows                                  |                      | Habilitado (essa configuração de política impede que dicas do Windows que está sendo mostrado aos usuários.)                                                                                                                                                                 |
| \***Conteúdo de nuvem**                                 | Desativar as experiências do cliente da Microsoft                                   |                      | Habilitado (se você habilitar essa configuração de política, os usuários não verão recomendações personalizadas da Microsoft e notificações sobre sua conta da Microsoft.)                                                                                                                                             |
| \***Coleta de dados e compilações de visualização**                            | Permitir telemetria                                           | 0 – segurança [Enterprise somente]                       | Habilitado (configuração de um valor de 0 se aplica a dispositivos que executam apenas as edições Enterprise, educação, IoT ou Windows Server.)                                                                                                                                                         |
| \***Coleta de dados e compilações de visualização**                            | Não mostrar notificações de comentários                                        |                      | Enabled                                                                                                                                                                                       |
| \***Coleta de dados e compilações de visualização**                            | Ativar/desativar o controle do usuário sobre compilações do Insider                                   |                      | Desabilitada                                                                                                                                                                                      |
| **Otimização de entrega**                           | Modo de Download                                             | Modo de download: Simples (99)           | 99 = modo de download simples sem emparelhamento. Otimização de entrega de baixa usando HTTP apenas e não tenta entrar em contato com os serviços de nuvem da otimização de entrega.                                                                                                                                          |
| **Gerenciador de janelas da área de trabalho**                          | Não permitir a invocação de Flip3D                            |                      | Enabled                                                                                                                                                                                       |
| **Gerenciador de janelas da área de trabalho**                          | Não permitir animações de janelas                            |                      | Enabled                                                                                                                                                                                       |
| **Gerenciador de janelas da área de trabalho**                          | Usar cor sólida para o plano de fundo de início                                      |                      | Enabled                                                                                                                                                                                       |
| **Edge UI**                                         | Permitir que o dedo da borda                                          |                      | Desativar                                                                                                                                                                                       |
| **Edge UI**                                         | Desabilitar as dicas de ajuda                                         |                      | Enabled                                                                                                                                                                                       |
| \***Explorador de arquivos**                                 | Configurar o Windows Defender SmartScreen                                    |                      | Desabilitado (SmartScreen será desativado para todos os usuários. Os usuários não serão avisados se tentarem executar aplicativos suspeitos da Internet.)                                                                                                                                                        |
|                                     |                                           |                      | **OBSERVAÇÃO**: Se não conectado à internet, isso impedirá que os computadores da tentativa de contatar a Microsoft para obter informações do SmartScreen.                                                                                                                                            |
| **Explorador de arquivos**                                   | Não mostrar o **novo aplicativo instalado** notificação                                  |                      | Enabled                                                                                                                                                                                       |
| \***Localizar meu dispositivo**                                | Ativar/desativar localizar meu dispositivo                                |                      | Desabilitado (quando encontrar meu dispositivo estiver desativado, o dispositivo e sua localização não estão registrados e a disposição de recurso encontrar meu dispositivo não funcione. O usuário também não será capaz de exibir o local do último uso do seu Active Directory digitalizador em seu dispositivo.)                                                                                                                             |
| **Gerenciador de jogos**                                   | Desativar o download de informações sobre o jogo                                  |                      | Enabled                                                                                                                                                                                       |
| **Gerenciador de jogos**                                   | Desabilitar atualizações de jogos                                     |                      | Enabled                                                                                                                                                                                       |
| **Gerenciador de jogos**                                   | Desativar o controle de última hora de jogos na pasta jogos                          |                      | Enabled                                                                                                                                                                                       |
| **Homegroup**                                       | Impedir que o computador ingresse em um grupo doméstico                             |                      | Enabled                                                                                                                                                                                       |
| \***Internet Explorer**                             | Permitir que os serviços Microsoft deem sugestões avançadas enquanto o usuário digita na barra de endereços             |                      | Desabilitado (os usuários não receberão sugestões aprimorados durante a digitação na barra de endereços. Além disso, os usuários não poderão alterar as sugestões de configuração.)                                                                                                                                       |
| **Internet Explorer**                               | Desabilitar a verificação periódica de atualizações de software do Internet Explorer                             |                      | Enabled                                                                                                                                                                                       |
| **Internet Explorer**                               | Desabilitar a exibição da tela inicial                         |                      | Enabled                                                                                                                                                                                       |
| **Internet Explorer**                               | Instalar novas versões do Internet Explorer automaticamente                                   |                      | Desabilitada                                                                                                                                                                                      |
| **Internet Explorer**                               | Impedir a participação no programa de Aperfeiçoamento da experiência do cliente                      |                      | Enabled                                                                                                                                                                                       |
| **Internet Explorer**                               | Impedir que o Assistente de primeira execução em execução                          | Vá diretamente para a home page             | Enabled                                                                                                                                                                                       |
| **Internet Explorer**                               | Definir o crescimento do processo de guia                                    | Baixo                  | Enabled                                                                                                                                                                                       |
| **Internet Explorer**                               | Especificar o comportamento padrão para uma nova guia                                    | Nova página da guia                         | Enabled                                                                                                                                                                                       |
| **Internet Explorer**                               | Desativar notificações de desempenho de complementos                                 |                      | Enabled                                                                                                                                                                                       |
| \***Internet Explorer**                             | Desativar o recurso de preenchimento automático para endereços da Web                      |                      | Habilitado (se você habilitar essa configuração de política, usuário não será sugerido corresponde ao inserir os endereços da Web. O usuário não pode alterar o preenchimento automático para a configuração de endereços da web.)                                                                                                                                                 |
| \***Internet Explorer**                             | Desativar a localização geográfica do navegador                              |                      | Habilitado (se você habilitar essa configuração de diretiva, suporte de localização geográfica do navegador é desativado.)                                                                                                                                                        |
| **Internet Explorer**                               | Desativar reabrir última sessão de navegação                                     |                      | Enabled                                                                                                                                                                                       |
| \***Internet Explorer**                             | Ative o recurso Sites Sugeridos                                   |                      | Desabilitado (se você desabilitar essa configuração de política, os pontos de entrada e a funcionalidade associada com esse recurso estão desativados.)                                                                                                                                                |
| **\*Internet Explorer** \\ exibição de compatibilidade                        | Desativar Modo de Exibição de Compatibilidade                               |                      | Habilitado (se você habilitar essa configuração de política, o usuário não é possível usar o botão de exibição de compatibilidade ou gerenciar a lista de sites do modo de exibição de compatibilidade.)                                                                                                                                                    |
| **Internet Explorer** \\ painel de controle da Internet**\\** página Avançado                  | Executar animações em páginas da web                              |                      | Desabilitada                                                                                                                                                                                      |
| **Internet Explorer** \\ painel de controle de Internet\\ página Avançado                      | Reproduzir vídeos em páginas da web                                  |                      | Desabilitada                                                                                                                                                                                      |
| **\*Internet Explorer** \\ painel de controle de Internet\\ página Avançado                    | Desativar o flip em frente com recursos de previsão de página                     |                      | Habilitado (a Microsoft coleta seu histórico de navegação para aprimorar como virar com a previsão de página funciona. Esse recurso não está disponível para o Internet Explorer para a área de trabalho. Se você habilitar essa configuração de política, flip prosseguir com a previsão de página está desativado e a próxima página da Web não está carregada em segundo plano.)                                                                                                           |
| **Internet Explorer** \\ as configurações da Internet\\ configurações avançadas\\ navegação                            | Desativar a detecção do número de telefone                           |                      | Enabled                                                                                                                                                                                       |
| **Internet Explorer** \\ as configurações da Internet\\ configurações avançadas\\ multimídia                          | Permitir que o Internet Explorer para reproduzir arquivos de mídia que usam os codecs alternativos                   |                      | Desabilitada                                                                                                                                                                                      |
| \***Localização e sensores**                          | Desativar local                                         |                      | Habilitado (f que você habilitar essa configuração de política, o recurso local é desativado e todos os programas neste computador são impedidos de usar as informações de localização do recurso de local).                                                                                                                                     |
| **Localização e sensores**                            | Desativar sensores                                          |                      | Enabled                                                                                                                                                                                       |
| **Locais e sensores /** localizador do Windows                               | Desativar o provedor do Windows local                                        |                      | Enabled                                                                                                                                                                                       |
| \***Mapas**                                          | Turn off Automatic Download and Update of Map Data                        |                      | Ativado (se você habilitar essa configuração em que o download automático e a atualização de dados de mapa está desativado).                                                                                                                                                              |
| \***Mapas**                                          | Desativar tráfego de rede não solicitado na página de configurações de Mapas Offline                    |                      | Ativado (se você habilitar essa configuração de política, os recursos que geram tráfego de rede nas configurações de mapas Offline página estão desativadas. Observação: Isso pode desativar toda a página de configurações.)                                                                                                                                        |
| \***Sistema de mensagens**                                     | Permitir sincronização de nuvem do serviço de mensagem                          |                      | Desabilitado (essa configuração de política permite backup e restauração de mensagens de texto de celular para serviços de nuvem da Microsoft).                                                                                                                                                             |
| \***Microsoft Edge**                                | Permitir sugestões de lista suspensa da Barra de endereços                              |                      | Desabilitada                                                                                                                                                                                      |
| \***Microsoft Edge**                                | Permitir atualizações de configuração para a Biblioteca de Livros                         |                      | Desabilitado (desativa as listas de compatibilidade no Microsoft Edge).                                                                                                                                                                    |
| \***Microsoft Edge**                                | Permitir que a lista de Compatibilidade da Microsoft                                        |                      | Desabilitado (se você desabilitar essa configuração, a lista de compatibilidade da Microsoft não é usada durante a navegação do navegador).                                                                                                                                                                |
| \***Microsoft Edge**                                | Permitir conteúdo Web na página Nova Guia                         |                      | Desabilitado (direciona Edge abrir com conteúdo em branco quando uma nova guia é aberta.)                                                                                                                                                                   |
| \***Microsoft Edge**                                | Configurar o preenchimento automático                                        |                      | Desabilitado (desabilita o Autopreenchimento na barra de endereço).                                                                                                                                                                   |
| \***Microsoft Edge**                                | Configurar Não Rastrear                                    |                      | Ativado (se você habilitar essa configuração, não rastrear solicitações sempre são enviadas aos sites solicitando informações de acompanhamento).                                                                                                                                                           |
| \***Microsoft Edge**                                | Configurar o Gerenciador de Senhas                                |                      | Desabilitado (se você desabilitar essa configuração, os funcionários não podem usar o Gerenciador de senhas para salvar suas senhas localmente.)                                                                                                                                                  |
| \***Microsoft Edge**                                | Configurar sugestões de pesquisa na barra de endereços                               |                      | Desabilitado (os usuários não podem ver sugestões de pesquisa no endereço barra do Microsoft Edge).                                                                                                                                                            |
| \***Microsoft Edge**                                | Configurar páginas Iniciar                                     |                      | Habilitado (se você habilitar essa configuração, você pode configurar uma ou mais páginas de início. Se essa configuração estiver habilitada, você também deve incluir URLs para as páginas, a separação de várias páginas usando os colchetes angulares neste formato: \<support.contoso.com\>\<support.microsoft.com\> Windows 10, versão 1703 ou posterior: Se você não quiser enviar o tráfego para a Microsoft, você pode usar o \<sobre: em branco\> configurado de valor, que será respeitada para dispositivos se associado a um domínio ou não, quando ele é a única URL.                                                                    |
| \***Microsoft Edge**                                | Configurar o Windows Defender SmartScreen                                    |                      | Desabilitado (Windows Defender SmartScreen estiver desativada e os funcionários não é possível ativá-lo.)                                                                                                                                                         |
|                                     |                                           |                      | **OBSERVAÇÃO**: Considere essa configuração dentro do ambiente. Se não conectado à Internet, isso impedirá que os computadores da tentativa de contatar a Microsoft para obter informações do SmartScreen.                                                                                                                                              |
| \***Microsoft Edge**                                | Impedir que a página da web de primeira execução seja aberto no Microsoft Edge                              |                      | **Habilitado** (usuários não verá a página de primeira execução ao abrir o Microsoft Edge pela primeira vez).                                                                                                                                                               |
| **OneDrive**                                        | Impedir que o OneDrive gerar tráfego de rede até que o usuário faz logon no OneDrive                      |                      | **Habilitado** (habilitar essa configuração impedir que o cliente de sincronização do OneDrive (OneDrive.exe) gerar tráfego de rede (a verificação de atualizações, etc.) até que o usuário faz logon no OneDrive ou inicia a sincronização de arquivos para o computador local).                                                                                                                           |
| \***OneDrive**                                      | Impedir o uso do OneDrive para armazenamento de arquivos                            |                      | **Habilitado** (a menos que o OneDrive é usado ou desativar local).                                                                                                                                                                  |
| **OneDrive**                                        | Salve documentos no OneDrive por padrão                                     |                      | **Desabilitado** (a menos que o OneDrive é usado ou desativar local).                                                                                                                                                                 |
| **RSS Feeds**                                       | Impedir que a descoberta automática de feeds e Web Slices                       |                      | **Enabled**                                                                                                                                                                                   |
| \***RSS Feeds**                                     | Desativar a sincronização em segundo plano de feeds e Web Slices                              |                      | **Habilitado** (se você habilitar essa configuração de diretiva, a capacidade de sincronizar feeds e Web Slices em segundo plano está desativado).                                                                                                                                              |
| \***Pesquisa**                                        | Permitir Cortana                                             |                      | **Desabilitado** (Cortana quando está desativada, os usuários ainda poderão usar a pesquisa para localizar itens no dispositivo.)                                                                                                                                                      |
| **Pesquisa**                                          | Permitir Cortana acima da tela de bloqueio                           |                      | **Desabilitado**                                                                                                                                                                                  |
| \***Pesquisa**                                        | Permitir que a Cortana e a pesquisa usem a localização                                  |                      | **Desabilitado**                                                                                                                                                                                  |
| **Pesquisa**                                          | Não permitir pesquisas na Web                                   |                      | **Enabled**                                                                                                                                                                                   |
| \***Pesquisa**                                        | Não pesquisar na web ou exibir os resultados da web na pesquisa                     |                      | **Habilitado** (se você habilitar essa configuração de política, consultas não serão realizadas na web e os resultados da web não serão exibidos quando um usuário executa uma consulta na pesquisa.)                                                                                                                                             |
| **Pesquisa**                                          | Evitar a adição de UNC locais para indexar a partir do painel de controle                                  |                      | **Enabled**                                                                                                                                                                                   |
| **Pesquisa**                                          | Impedir a indexação de arquivos no cache de arquivos offline                             |                      | **Enabled**                                                                                                                                                                                   |
| \***Pesquisa**                                        | Definir quais informações são compartilhadas na Pesquisa                                  | Informações anônimas                       | **Habilitado** (compartilhar informações de uso, mas não compartilham o histórico de pesquisa, informações de conta da Microsoft ou local específico.)                                                                                                                                                              |
| \***Plataforma de proteção de software**                                  | Desativar a validação AVC Online de cliente KMS                                 |                      | **Habilitado** (habilitar essa configuração impede que o computador enviando dados à Microsoft sobre seu estado de ativação.)                                                                                                                                                      |
| \***Conversão de fala**                                        | Permitir atualização automática dos dados de controle por voz                                     |                      | **Desabilitado** (será não periodicamente verificação para modelos de fala atualizado)                                                                                                                                                                          |
| \***armazenar**                                         | Desativar o download automático e a instalação de atualizações                        |                      | **Habilitado** (se você habilitar essa configuração, o download automático e instalação de atualizações de aplicativo é desativado.)                                                                                                                                                                |
| \***armazenar**                                         | Desativar o Download automático de atualizações em dispositivos Win8                                   |                      | **Habilitado** (se você habilitar essa configuração, o download automático de atualizações de aplicativos é desligado).                                                                                                                                                                 |
| **Store**                                           | Desativar a oferta para atualizar para a versão mais recente do Windows                             |                      | **Enabled**                                                                                                                                                                                   |
| \***Sincronizar suas configurações**                            | Não sincronizar                               | Permitir que os usuários ativar a sincronização (não selecionado)         | **Habilitado** (se você habilitar essa configuração de política, "sincronizar suas configurações de" será desativado e nenhum dos grupos "sincronizar sua configuração de" serão sincronizados neste dispositivo.                                                                                                                                                |
| **Entrada de texto**                                      | Melhorar o reconhecimento de digitação e escrita à tinta                                     |                      | **Desabilitado**                                                                                                                                                                                  |
| **Windows Defender antivírus** \\ mapas                               | Ingressar no Mapas Microsoft                                       |                      | **Desabilitado** (se você desabilitar ou não definir essa configuração, não será unir Microsoft MAPS.)                                                                                                                                                             |
| **Windows Defender antivírus** \\ mapas                               | Enviar amostras de arquivo quando outra análise for necessária                       | Nunca enviar                           | **Habilitado** (somente se não tiver optado-in para dados de diagnóstico de mapas)                                                                                                                                                                         |
| **Windows Defender antivírus** \\ Reporting                          | Desativar notificações aprimoradas                           |                      | **Habilitado** (se você habilitar essa configuração, as notificações do Windows Defender antivírus avançada não exibirá em clientes.)                                                                                                                                                       |
| **Windows Defender antivírus** \\ atualizações de assinatura                                  | Definir a ordem das origens para baixar atualizações de definições                            | FileShares                           | **Habilitado** (se você habilitar essa configuração, as origens de atualização de definição serão contatadas na ordem especificada. Depois que as atualizações de definições baixou com êxito de uma origem especificada, as fontes restantes na lista serão não ser contatadas.)                                                                                                                    |
| **Relatório de erros do Windows**                         | Enviar automaticamente os despejos de memória para relatórios de erros gerados pelo sistema operacional                            |                      | **Desabilitado**                                                                                                                                                                                  |
| **Relatório de erros do Windows**                         | Desabilitar o Relatório de Erros do Windows                           |                      | **Enabled**                                                                                                                                                                                   |
| **Jogo da Windows registrar e transmitir**                         | Habilita ou desabilita o jogo do Windows registrar e transmitir                               |                      | **Desabilitado**                                                                                                                                                                                  |
| **Windows Installer**                               | Controle o tamanho máximo do cache de arquivos de linha de base                               | 5                    | **Enabled**                                                                                                                                                                                   |
| **Windows Installer**                               | Desativar a criação de pontos de verificação de restauração do sistema                           |                      | **Enabled**                                                                                                                                                                                   |
| **Windows Mail**                                    | Desativar o recurso de comunidades                          |                      | **Enabled**                                                                                                                                                                                   |
| **Windows Media Player**                            | Não mostrar caixas de diálogo do primeiro uso                                        |                      | **Enabled**                                                                                                                                                                                   |
| **Windows Media Player**                            | Impedir o compartilhamento de mídia                                     |                      | **Enabled**                                                                                                                                                                                   |
| **Windows Mobility Center**                         | Desativar o Windows Mobility Center                          |                      | **Enabled**                                                                                                                                                                                   |
| **Análise de confiabilidade do Windows**                                    | Configurar provedores WMI de confiabilidade                                       |                      | **Desabilitado**                                                                                                                                                                                  |
| **Windows Update**                                  | Permitir instalação imediata de atualizações automáticas                            |                      | **Enabled**                                                                                                                                                                                   |
| **Windows Update**                                  | Não se conectar a locais de Internet do Windows Update                                   |                      | **Habilitado** (a habilitação dessa política desabilitará essa funcionalidade e pode fazer com que a conexão para serviços públicos, como a Windows Store para parar de funcionar. **Observação:** Essa política se aplica somente quando este dispositivo está configurado para se conectar a um serviço de atualização da intranet usando a política "Especificar intranet local do serviço do Microsoft update".                                                                                                           |
| **Windows Update**                                  | Remover o acesso a todos os recursos de atualização do Windows                              |                      | **Enabled**                                                                                                                                                                                   |
| **\*Atualização do Windows** \\ Windows Update for Business                                  | Gerenciar compilações de visualização                                     | Defina o comportamento de recebimento das compilações de visualização:       | **Habilitada** (selecionando **compilações do preview Disable** impedirá que as compilações de visualização seja instalado no dispositivo. Isso impedirá que os usuários de optar por programa Windows Insider, por meio das configurações -\> atualização e segurança.)                                                                                                                                    |
|                                     |                                           | Desabilitar compilações de visualização               |                                                                                                                                                                               |
| **\*Atualização do Windows** \\ Windows Update for Business                                  | Selecione quando as compilações de visualização e atualizações de recurso são recebidas                               | Canal Semestral                 | **Habilitado** (habilitar essa política especificar o nível de compilação de visualização ou atualizações de recurso para receber e quando.)                                                                                                                                                                |
|                                     |                                           | E adiamentos: 365 dias,                 |                                                                                                                                                                               |
|                                     |                                           | Pausar start: aaaa-mm-dd              |                                                                                                                                                                               |
| **Atualização do Windows** \\ Windows Update for Business                    | Selecione quando as atualizações de qualidade são recebidas                                  | 1. 30 dias 2. Pausar qualidade atualiza inicial aaaa-mm-dd              | **Enabled**                                                                                                                                                                                   |
| **Configurações de política personalizada do tráfego de restrita do Windows**                               | Impedir que o OneDrive gerar tráfego de rede até que o usuário faz logon no OneDrive                      |                      | **Habilitado** (habilitar essa configuração se você quiser impedir que o cliente de sincronização do OneDrive (OneDrive.exe) de tráfego de rede (a verificação de atualizações, etc.) até que o usuário faz logon no OneDrive ou inicia a sincronização de arquivos para o computador local).                                                                                                                         |
| **Configurações de política personalizada do tráfego de restrita do Windows**                               | Desativar as notificações do Windows Defender                                   |                      | **Habilitado** (se você habilitar essa configuração de política, o Windows Defender não enviará notificações com informações críticas sobre a integridade e a segurança do seu dispositivo.)                                                                                                                                          |
| **Política do computador local \\ configuração do usuário \\ modelos administrativos**                         |                                           |                      |                                                                                                                                                                               |
| **Painel de controle** \\ opções regionais e idioma                                   | Desativar a oferta de previsões de texto ao digitar                                 |                      | **Enabled**                                                                                                                                                                                   |
| **Área de Trabalho**                                         | Não adicionar compartilhamentos de documentos abertos recentemente para locais de rede                       |                      | **Enabled**                                                                                                                                                                                   |
| **Área de Trabalho**                                         | Desativar a janela Aero Shake minimizando o gesto do mouse                       |                      | **Enabled**                                                                                                                                                                                   |
| **Área de trabalho** / Active Directory                                      | Tamanho máximo de pesquisas do Active Directory                                 | 2500                 | **Enabled**                                                                                                                                                                                   |
| **Menu Iniciar e barra de tarefas**                          | Não permitir a fixação app Store na barra de tarefas                             |                      | **Enabled**                                                                                                                                                                                   |
| **Menu Iniciar e barra de tarefas**                          | Não exibir nem controlar itens nas Listas de Atalhos a partir de locais remotos                         |                      | **Enabled**                                                                                                                                                                                   |
| **Menu Iniciar e barra de tarefas**                          | Não use o método baseado em pesquisa ao resolver atalhos do shell                         |                      | **Habilitado** (o sistema não realizar a pesquisa final na unidade. Ele apenas exibirá uma mensagem explicando que o arquivo não foi encontrado.)                                                                                                                                            |
| **Menu Iniciar e barra de tarefas**                          | Remova a barra de pessoas na barra de tarefas                                    |                      | **Habilitado** (o ícone de pessoas será removido da barra de tarefas, a alternância de configurações correspondente é removida da página de configurações de barra de tarefas e os usuários não poderão às pessoas Fixar na barra de tarefas).                                                                                                                                           |
| **Menu Iniciar e barra de tarefas**                          | Desativar as notificações de balão de anúncio do recurso                      |                      | **Habilitado** (usuários não é possível fixar o aplicativo Store na barra de tarefas. Se o aplicativo Store já está fixado na barra de tarefas, ele será removido da barra de tarefas na próxima vez que entrar.)                                                                                                                                             |
| **Menu Iniciar e barra de tarefas**                          | Desativar o controle do usuário                                    |                      | **Enabled**                                                                                                                                                                                   |
| **Menu Iniciar e barra de tarefas** / notificações                          | Desativar as notificações do sistema                              |                      | **Enabled**                                                                                                                                                                                   |
| **Componentes do Windows** / conteúdo de nuvem                              | Desativar todos os recursos de Destaque do Windows                                   |                      | **Enabled**                                                                                                                                                                                   |
| **Edge UI**                                         | Desativar o controle de uso do aplicativo                            |                      | **Enabled**                                                                                                                                                                                   |
| **Explorador de arquivos**                                   | Desativar o cache de imagens em miniatura                                    |                      | **Enabled**                                                                                                                                                                                   |
| **Explorador de arquivos**                                   | Desativar exibição de entradas recentes de pesquisa na caixa de pesquisa do Explorador de arquivos                 |                      | **Enabled**                                                                                                                                                                                   |
| **Explorador de arquivos**                                   | Desativar o cache de miniaturas no arquivo Thumbs oculto.                               |                      | **Enabled**                                                                                                                                                                                   |




### <a name="notes-about-network-connectivity-status-indicator"></a>Observações sobre o indicador de Status de conectividade de rede

As configurações de diretiva de grupo acima incluem configurações para desativar a verificação para ver se o sistema está conectado à Internet. Se seu ambiente não se conecta à Internet em todos os ou conecta-se indiretamente, você pode definir uma configuração de diretiva de grupo para remover o ícone de rede na barra de tarefas. O motivo pelo qual você talvez queira remover a ícone na barra de tarefas é se você desative a conectividade com a Internet de rede verifica, haverá um sinalizador amarelo no ícone de rede, mesmo que a rede pode estar funcionando normalmente. Se você quiser remover o ícone de rede como uma configuração de diretiva de grupo, você pode encontrar que neste local:

| Atualização do Windows ou Windows Update for Business                | Selecione quando as atualizações de qualidade são recebidas | 1. 30 dias 2. Pausar qualidade atualiza inicial aaaa-mm-dd | Enabled                             |
|-----------------------------------------------------------------------------|------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------------------------|
| **Política do computador local \\ configuração do usuário \\ modelos administrativos** |          |                         |                     |
| **Menu Iniciar e barra de tarefas**                  | Remover o ícone de rede               |                         | **Habilitado** (o ícone de rede não é exibido na área de notificação do sistema.) |

Para obter mais informações sobre a rede Conexão Status NCSI (indicador), consulte: [O ícone de Status de Conexão de rede](https://blogs.technet.microsoft.com/networking/2012/12/20/the-network-connection-status-icon/)

### <a name="system-services"></a>Serviços do sistema

Se você estiver considerando a desabilitação de serviços do sistema para conservar os recursos, tome muito cuidado para que o serviço que está sendo considerado não está de alguma forma de um componente de algum outro serviço.

Além disso, a maioria dessas recomendações espelha as recomendações para o Windows Server 2016 com experiência Desktop; Para obter mais informações, consulte [orientações sobre a desabilitação de serviços do sistema no Windows Server 2016 com experiência Desktop](https://docs.microsoft.com/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server).

Observe que muitos serviços que podem parecer estar bons candidatos para desabilitar estão definidas para o tipo de inicialização manual do serviço. Isso significa que o serviço não será iniciado automaticamente e não for iniciado, a menos que um aplicativo ou serviço específico dispara uma solicitação para o serviço que está sendo considerados para desabilitar. Serviços que já estão definidos para iniciar o manual de tipo não são geralmente listados aqui.

| Serviço do Windows                                                                                                                               | Item                                                                                     | Comentário                                                                            |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CDPUserService                                                                                                                                | Esse serviço de usuário é usado para cenários de plataformas de dispositivos conectados                                                                       | OBSERVAÇÃO: Esse é um serviço por usuário e como tal, o *serviço de modelo* deve ser desabilitada.                                                          |
| Experiências de usuário conectado e telemetria                                                                                                                      | Habilita os recursos que dão suporte a experiências de usuário no aplicativo e conectado. Além disso, esse serviço gerencia a coleção orientada a eventos e a transmissão de informações de diagnóstico e de uso (usadas para melhorar a experiência e a qualidade da plataforma do Windows) quando o diagnóstico e as configurações de opção de privacidade de uso são habilitadas em Comentários e diagnósticos. | Considere desabilitar se na rede desconectado                                                                      |
| Dados de contato                                                                                                                                  | Dados de contato de índices para a pesquisa rápida de contato. Se você parar ou desabilitar esse serviço, os contatos podem estar ausentes dos resultados da pesquisa.                                                                | (PimIndexMaintenanceSvc) OBSERVAÇÃO: Esse é um serviço por usuário e como tal, o *serviço de modelo* deve ser desabilitada.              |
| Serviço de diretiva de diagnóstico                                                                                                                     | Habilita a detecção de problemas, solução de problemas e resolução para componentes do Windows. Se esse serviço for interrompido, diagnóstico deixará de funcionar.                                                       |                                                                                    |
| Gerenciador de mapas baixado                                                                                                                       | Serviço do Windows para acesso a aplicativos para mapas baixados. Esse serviço é iniciado sob demanda pelo aplicativo acessando baixado mapas. A desabilitação desse serviço impedirá que aplicativos acessem mapas.                                                     |                                                                                    |
| Serviço de Geolocalização                                                                                                                           | Monitora o local atual do sistema e gerencia os limites geográficos                                                                        |                                                                                    |
| Serviço de GameDVR e transmissão de usuário                                                                                                                            | Esse serviço de usuário é usado para gravações de jogo e transmissões ao vivo                                                                        | OBSERVAÇÃO: Esse é um serviço por usuário e como tal, o serviço de modelo deve ser desabilitado.                                                            |
| MessagingService                                                                                                                              | Serviço de suporte a mensagens de texto e funcionalidades relacionadas.                                                                             | OBSERVAÇÃO: Esse é um serviço por usuário e como tal, o *serviço de modelo* deve ser desabilitada.                                                          |
| Otimizar unidades                                                                                                                               | Ajuda o computador a executar com mais eficiência ao otimizar arquivos em unidades de armazenamento.                                                                           | Soluções de VDI não normalmente se beneficiam da otimização de disco. Essas unidades de"" não são unidades tradicionais e com frequência, apenas uma alocação de armazenamento temporário.                                               |
| Superfetch                                                                                                                                    | Mantém e melhora o desempenho do sistema ao longo do tempo.                                                                                     | Em geral não melhorar o desempenho em VDI, especialmente não persistente, considerando que o estado do sistema operacional será descartado cada reinicialização.                                         |
| Teclado de toque e o serviço do painel de manuscrito                                                                                                                  | Habilita a funcionalidade de caneta e tinta de teclado de toque e o painel de manuscrito                                                                                   |                                                                                    |
| Relatório de erros do Windows                                                                                                                       | Permite que os erros sejam relatados quando programas parar de funcionar ou de responder e permite que as soluções existentes sejam entregues. Também permite que os logs a serem gerados para diagnóstico e reparar os serviços. Se esse serviço for interrompido, relatório de erros pode não funcionar corretamente e resultados de serviços de diagnóstico e reparos podem não ser exibidos.                   | Com o VDI, diagnóstico geralmente é executado em um cenário offline e não em produção base. E, além disso, alguns clientes desabilitar o WER mesmo assim. WER incorre em uma pequena quantidade de recursos para muitas coisas diferentes, incluindo falha ao instalar um dispositivo ou Falha ao instalar uma atualização. |
| Serviço de Compartilhamento de Rede do Windows Media Player                                                                                                                  | Compartilhamentos de bibliotecas do Windows Media Player para outros jogadores em rede e dispositivos de mídia usando o Plug and Play Universal                                                                         | Não é necessária, a menos que os clientes estão compartilhando bibliotecas WMP na rede.                                                              |
| Serviço de ponto de acesso móvel do Windows                                                                                                                                | Fornece a capacidade de compartilhar uma conexão de dados de celular com outro dispositivo.                                                                            |                                                                                    |
| Windows Search                                                                                                                                | Fornece a indexação de conteúdo, o cache de propriedade e os resultados da pesquisa para arquivos, email e outros tipos de conteúdo.                                                                    | Provavelmente não é necessária especialmente com VDI não persistente                                                             |

#### <a name="per-user-services-in-windows"></a>Serviços por usuário no Windows
[Serviços por usuário](https://docs.microsoft.com/windows/application-management/per-user-services-in-windows) são serviços que são criados quando um usuário entra no Windows ou Windows Server e é interrompido e excluído quando o usuário sai. Esses serviços são executados no contexto de segurança da conta de usuário - isso fornece um melhor gerenciamento de recursos que a abordagem anterior de executar esses tipos de serviços no Gerenciador, associada a uma conta pré-configurada ou como tarefas. 

### <a name="scheduled-tasks"></a>Tarefas Agendadas

Como outros itens no Windows, certifique-se de que um item não é necessária antes de desabilitá-lo.

A seguinte lista de tarefas são aqueles que executam as coleções de dados ou otimizações em computadores que mantêm seu estado entre as reinicializações. Quando uma tarefa de VDI VM reinicia e descarta todas as alterações desde a última inicialização, otimizações relacionadas a computadores físicos não são úteis.

Você pode obter todas as tarefas agendadas atuais, incluindo descrições, com o seguinte código do PowerShell:

`Get-ScheduledTask | Select-Object -Property TaskPath,TaskName,State,Description |Export-CSV -Path C:\Temp\W10_1803_SchTasks.csv -NoTypeInformation`

Válido **nome da tarefa agendada** valores incluem:

- Tarefa de atualização do OneDrive autônoma v2
- Avaliador de compatibilidade da Microsoft
- ProgramDataUpdater
- StartupAppTask
- CleanupTemporaryState
- Proxy
- UninstallDeviceTask
- ProactiveScan
- Consolidador
- UsbCeip
- Verificação de integridade de dados
- Verificação de integridade de dados para recuperação de pane
- ScheduledDefrag
- SilentCleanup
- Microsoft-Windows-DiskDiagnosticDataCollector
- Diagnóstico
- StorageSense
- DmClient
- DmClientOnScenarioDownload
- Histórico de arquivos (modo de manutenção)
- ScanForUpdates
- ScanForUpdatesAsUser
- SmartRetry
- Notificações
- WindowsActionDialog
- Celular do WinSAT
- MapsToastTask
- ProcessMemoryDiagnosticEvents
- RunFullMemoryDiagnostic
- Analisador de metadados MNO
- LPRemove
- GatherNetworkInfo
- WiFiTask
- Tarefas de SQM
- AnalyzeSystem
- MobilityManager
- VerifyWinRE
- RegIdleBackup
- FamilySafetyMonitor
- FamilySafetyRefreshTask
- IndexerAutomaticMaintenance
- SpaceAgentTask
- SpaceManagerTask
- HeadsetButtonPress
- SpeechModelDownloadTask
- ResPriStaticDbSync
- WsSwapAssessmentTask
- SR
- SynchronizeTimeZone
- Notificações de USB
- QueueReporting
- UpdateLibrary
- Início agendado
- sih
- XblGameSaveTask

### <a name="apply-windows-and-other-updates"></a>Aplicar o Windows e outras atualizações

Se no Microsoft Update ou de seus recursos internos, aplica atualizações disponíveis, incluindo assinaturas do Windows Defender. Isso é um bom momento para aplicar outras atualizações disponíveis, incluindo aqueles para o Microsoft Office se instalado.

### <a name="automatic-windows-traces"></a>Rastreamentos automática do Windows

Windows está configurado, por padrão, para coletar e salvar dados de diagnóstico limitados. O objetivo é habilitar o diagnóstico, ou gravar dados no caso de solução de problemas adicional é necessária. Você pode encontrar os rastreamentos do sistema automático iniciando o aplicativo de gerenciamento do computador e, em seguida, expandindo **ferramentas do sistema**, **desempenho**, **conjuntos de Coletores de dados**e, em seguida, selecionando **sessões de rastreamento de evento**.


Alguns dos rastreamentos exibidos sob **sessões de rastreamento de eventos** e **sessões de rastreamento de eventos de inicialização** não pode e não deve ser interrompido. Outros, como o **WiFiSession** rastreamento pode ser interrompido. Para interromper um rastreamento em execução sob **sessões de rastreamento de eventos** o rastreamento com o botão direito e, em seguida, selecione **parar**. Para impedir que os rastreamentos iniciado automaticamente na inicialização, siga estas etapas:

1.  Selecione o **sessões de rastreamento de eventos de inicialização** pasta

2.  Localize o rastreamento de seu interesse e, em seguida, clique duas vezes em que o rastreamento.

3.  Selecione o **sessão de rastreamento** guia.

4.  Desmarque a caixa rotulada **Enabled**. 

5.  Selecione **OK**.

Aqui estão alguns rastreamentos do sistema deve considerar a desativação para o uso VDI:

| Nome                    | Comentário                       |
|-------------------------|-----------------------------------------------|
| AppModel                | Uma coleção de rastreamentos, um dos quais é o telefone |
| CloudExperienceHostOOBE |               |
| DiagLog                 |               |
| NtfsLog                 |               |
| TileStore               |               |
| UBPM                    |               |
| WiFiDriverIHVSession    | Se não usar um dispositivo de Wi-Fi                    |
| WiFiSession             |               |

#### <a name="servicing-the-operating-system-and-apps"></a>O sistema operacional e aplicativos de serviço

Em algum momento durante o processo de otimização de imagem, as atualizações disponíveis do Windows devem ser aplicadas. Você pode definir o Windows Update para instalar atualizações para outros produtos da Microsoft, bem como o Windows. Para definir isso, abra **configurações do Windows**, em seguida, selecione **atualização e segurança**e, em seguida, selecione **opções avançadas**. Selecione **fornecer atualizações para outros produtos da Microsoft quando eu atualizar o Windows** defini-lo como **em**.

Isso seria uma boa configuração caso você pretende instalar aplicativos da Microsoft como o Microsoft Office à imagem base. Dessa forma Office é atualizado quando a imagem é colocada no serviço. Também há atualizações do .NET e determinados componentes não são da Microsoft, como Adobe que possuem atualizações disponíveis por meio do Windows Update.

Uma consideração muito importante para VMs de VDI não persistentes são atualizações de segurança, incluindo arquivos de definição de software de segurança. Essas atualizações talvez seja liberadas uma vez ou até mesmo mais de uma vez por dia. Pode haver uma maneira de manter essas atualizações, incluindo o Windows Defender e componentes não-Microsoft.

Para o Windows Defender pode ser melhor permitir que as atualizações ocorram, mesmo em VDI não persistente. As atualizações serão aplicadas a praticamente cada sessão de logon, mas as atualizações são pequenas e não devem ser um problema. Além disso, a VM não será por trás de atualizações porque serão aplicadas somente a versão mais recente disponível. O mesmo seria verdadeiro para arquivos de definição de não-Microsoft.

> [!NOTE]  
> Store atualização de aplicativos (aplicativos UWP) por meio do Windows Store. Atualizam as versões atuais do Office como o Office 365 por meio de seus próprios mecanismos quando diretamente conectado à Internet ou por meio de tecnologias de gerenciamento quando não.

### <a name="windows-defender-optimization-with-vdi"></a>Otimização do Windows Defender com VDI

A Microsoft publicou recentemente documentação relacionada ao Windows Defender em um ambiente de VDI. Ver [guia de implantação do Windows Defender antivírus em um ambiente de infraestrutura de área de trabalho virtual (VDI)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus) para obter detalhes.

O artigo acima contém procedimentos para fazer a manutenção de imagem de ouro de VDI e como manter os clientes VDI, pois eles estão em execução. Para reduzir a largura de banda de rede quando computadores VDI precisarão atualizar suas assinaturas do Windows Defender, escalonar reinicializações e agenda é reinicializado durante horários de sempre que possível. As atualizações de assinatura do Windows Defender podem estar contidas internamente em compartilhamentos de arquivos e quando for prático, ter esses compartilhamentos de arquivos nos segmentos de rede fechados ou mesmos que as máquinas virtuais VDI.

Consulte o documento listado no início desta seção para obter muito mais informações sobre como otimizar o Windows Defender com VDI.

### <a name="tuning-windows-10-network-performance-by-using-registry-settings"></a>Ajustando o desempenho de rede do Windows 10 usando as configurações do registro

Isso é especialmente importante em ambientes em que o computador físico ou VDI tem uma carga de trabalho que é principalmente com base em rede. As configurações de desempenho de tendência esta seção para favorecer as conexões de rede, configurando o armazenamento em buffer e o armazenamento em cache das coisas adicionais como entradas de diretório e assim por diante.

Observe que algumas configurações nesta seção são *baseada no registro somente* e deve ser incorporado na imagem de base antes da imagem é implantada para uso em produção.

As configurações a seguir estão documentadas na [diretriz de ajuste de desempenho do Windows Server 2016](https://docs.microsoft.com/windows-server/administration/performance-tuning/) informações, publicadas no site Microsoft.com pelo grupo de produtos do Windows.

#### <a name="disablebandwidththrottling"></a>DisableBandwidthThrottling

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\DisableBandwidthThrottling

Aplica-se ao Windows 10. O padrão é **0**. Por padrão, o redirecionador SMB limita a taxa de transferência em conexões de rede de alta latência, em alguns casos, para evitar tempos limite relacionados à rede. Definir esse valor de registro a **1** desabilita essa limitação, permitindo maior taxa de transferência de arquivo sobre conexões de rede de alta latência, portanto, você deve considerar essa configuração.

#### <a name="fileinfocacheentriesmax"></a>FileInfoCacheEntriesMax

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\FileInfoCacheEntriesMax

Aplica-se ao Windows 10. O padrão é **64**, com um intervalo válido de 1 a 65536. Esse valor é usado para determinar a quantidade de metadados de arquivo que pode ser armazenada em cache pelo cliente. Aumentar o valor pode reduzir o tráfego de rede e aumentar o desempenho quando muitos arquivos são acessados. Tente aumentar esse valor para **1024**.

#### <a name="directorycacheentriesmax"></a>DirectoryCacheEntriesMax

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\DirectoryCacheEntriesMax

Aplica-se ao Windows 10. O padrão é **16**, com um intervalo válido de 1 a 4096. Esse valor é usado para determinar a quantidade de informações de diretório que pode ser armazenada em cache pelo cliente. Aumentar o valor pode reduzir o tráfego de rede e aumentar o desempenho quando diretórios grandes são acessados. Considere aumentar esse valor para **1024**.

#### <a name="filenotfoundcacheentriesmax"></a>FileNotFoundCacheEntriesMax

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\FileNotFoundCacheEntriesMax

Aplica-se ao Windows 10. O padrão é **128**, com um intervalo válido de 1 a 65536. Esse valor é usado para determinar a quantidade de informações de nome de arquivo que pode ser armazenada em cache pelo cliente. Aumentar o valor pode reduzir o tráfego de rede e aumentar o desempenho quando muitos nomes de arquivo são acessados. Considere aumentar esse valor para **2048**.

#### <a name="dormantfilelimit"></a>DormantFileLimit

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\DormantFileLimit

Aplica-se ao Windows 10. O padrão é **1023**. Esse parâmetro especifica o número máximo de arquivos que deve ser aberto em um recurso compartilhado após o aplicativo fechar o arquivo. Onde vários milhares de clientes estiver se conectando a servidores SMB, considere a possibilidade de reduzir esse valor para **256**.

Você pode configurar várias dessas configurações de SMB usando o [SmbClientConfiguration conjunto](https://docs.microsoft.com/powershell/module/smbshare/set-smbclientconfiguration) e [SmbServerConfiguration conjunto](https://docs.microsoft.com/powershell/module/smbshare/set-smbserverconfiguration) cmdlets do Windows PowerShell. Você pode configurar as configurações de registro usando o Windows PowerShell também, como no exemplo a seguir:

`Set-ItemProperty -Path "HKLM:\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters" RequireSecuritySignature -Value 0 -Force`

### <a name="additional-settings-from-the-windows-restricted-traffic-limited-functionality-baseline-guidance"></a>Configurações adicionais com as diretrizes do Windows restrita tráfego limitado a funcionalidade da linha de base

A Microsoft lançou uma linha de base criada usando os mesmos procedimentos como o [linhas de base de segurança Windows](https://docs.microsoft.com/windows/device-security/windows-security-baselines), para ambientes que não estão conectados diretamente à Internet ou se desejam reduzir os dados enviados à Microsoft e outros serviços.

O [Windows restrito tráfego limitado funcionalidade de linha de base](https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services) configurações são marcadas na tabela de diretiva de grupo com um asterisco.

### <a name="disk-cleanup-including-using-the-disk-cleanup-wizard"></a>Limpeza de disco (incluindo usando o Assistente de limpeza de disco)

Limpeza de disco pode ser especialmente útil com implementações de VDI da imagem mestra. Depois que a imagem mestra é preparada, atualizada e configurada, uma das tarefas para executar a última é a limpeza de disco. O Assistente de limpeza de disco incorporado Windows pode ajudar a limpar a maioria das áreas de potencial de economia de espaço em disco.

> [!NOTE]  
> O Assistente para limpeza de disco não está sendo desenvolvido. Windows usará outros métodos para fornecer funções de limpeza de disco.



Aqui estão sugestões para várias tarefas de limpeza de disco. Você deve testar esses antes de implementar qualquer uma delas:

1.  Execute o Assistente de limpeza de disco (elevado) após a aplicação de todas as atualizações. Incluir as categorias **otimização de entrega** e **limpeza de atualização do Windows**. Você pode automatizar esse processo com **Cleanmgr.exe** com o **/sageset: 11** opção. Essa opção define valores de registro que podem ser usados posteriormente para automatizar a limpeza de disco, usando todas as opções disponíveis no Assistente de limpeza de disco.

    1.  Em uma VM, de teste em uma instalação limpa, executando **/sageset: 11 de Cleanmgr.exe** revela que há apenas duas opções de limpeza de disco automático habilitadas por padrão:

    - Arquivos de programas baixados

    - Arquivos temporários da Internet

    2.  Se você definir mais opções, ou todas as opções, essas opções são registradas no registro, acordo com o valor de índice fornecido no comando anterior ( **/sageset: 11 de Cleanmgr.exe**). Neste exemplo, usamos o valor *11* como nosso índice, para um procedimento de limpeza de disco automatizada subsequentes.

    3.  Depois de executar **/sageset: 11 de Cleanmgr.exe** você verá um número de categorias de opções de limpeza de disco. Você pode selecionar todas as opções e, em seguida, selecione **Okey**. Você observará que o Assistente para limpeza de disco apenas desaparece. No entanto, as configurações selecionadas são salvas no registro e pode ser invocadas executando **/sagerun: 11 de Cleanmgr.exe**.

2.  Limpe o armazenamento de cópia de sombra de Volume, se qualquer um estiver em uso. Para fazer isso, execute os seguintes comandos em um prompt elevado:

    - **vssadmin list shadows**

    - **Vssadmin lista shadowstorage**

        Se a saída desses comandos for *não foram encontrados itens que satisfazem a consulta.* , em seguida, não há nenhum armazenamento VSS em uso.

3.  Logs e arquivos temporários de limpeza. Em um prompt de comando com privilégios elevados, execute estes comandos:

    - **/DEL c:\\\*. tmp /s**

    - **/DEL c:\\Windows\\Temp\\.**

    - **DEL % temp %\\.**

4.  Exclua qualquer perfil não utilizados no sistema com este comando:

    **wmic path win32_UserProfile where LocalPath="c:\\\\users\\\\\<user\>" Delete**

### <a name="remove-onedrive"></a>Remover o OneDrive

Remover OneDrive envolve a remoção do pacote, desinstalar e remover \*arquivos. lnk. Você pode usar o código PowerShell de exemplo a seguir para ajudá-lo na remoção OneDrive a partir da imagem:

```azurecli

Taskkill.exe /F /IM "OneDrive.exe"
Taskkill.exe /F /IM "Explorer.exe"` 
    if (Test-Path "C:\\Windows\\System32\\OneDriveSetup.exe")`
     { Start-Process "C:\\Windows\\System32\\OneDriveSetup.exe"`
         -ArgumentList "/uninstall"`
         -Wait }
    if (Test-Path "C:\\Windows\\SysWOW64\\OneDriveSetup.exe")`
     { Start-Process "C:\\Windows\\SysWOW64\\OneDriveSetup.exe"`
         -ArgumentList "/uninstall"`
         -Wait }
Remove-Item -Path
"C:\\Windows\\ServiceProfiles\\LocalService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force
Remove-Item -Path "C:\\Windows\\ServiceProfiles\\NetworkService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force \# Remove the automatic start item for OneDrive from the default user profile registry hive
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Load HKLM\\Temp C:\\Users\\Default\\NTUSER.DAT" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Delete HKLM\\Temp\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run /v OneDriveSetup /f" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Unload HKLM\\Temp" -Wait Start-Process -FilePath C:\\Windows\\Explorer.exe -Wait
```


Para perguntas ou dúvidas sobre as informações neste artigo, entre em contato com a equipe de contas da Microsoft, pesquise o blog do Microsoft VDI, postar uma mensagem em fóruns da Microsoft ou entre em contato com a Microsoft para fazer perguntas ou preocupações.