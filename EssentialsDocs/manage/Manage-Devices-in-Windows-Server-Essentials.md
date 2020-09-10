---
title: Gerenciar Dispositivos no Windows Server Essentials
description: Descreve como usar o Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f5fe1088-ebe7-4799-a47d-075b0048dea1
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 96d99bb41a528a3a2f86be2d876df6e777e4b790
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623142"
---
# <a name="manage-devices-in-windows-server-essentials"></a>Gerenciar Dispositivos no Windows Server Essentials

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 As seções a seguir abordam os recursos de gerenciamento de dispositivo de um servidor e explicam como configurar e usar dispositivos na sua rede:

-   [Gerenciar dispositivos usando o Painel](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_1)

-   [Atribuir permissão para fazer logon nos computadores de rede específicos de contas de usuário](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_2)

-   [Remover um computador do servidor](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)

-   [Definir configurações de política de grupo para redirecionamento de pasta e de segurança](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_5)

-   [Conectar-se a um computador da rede por meio de uma sessão de área de trabalho remota](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_7)

-   [Exibir as propriedades do computador](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_8)

##  <a name="manage-devices-by-using-the-dashboard"></a><a name="BKMK_1"></a> Gerenciar dispositivos usando o painel
 O Windows Server Essentials torna possível executar tarefas administrativas comuns usando o Painel do Windows Server Essentials. A página **Dispositivos** do Painel fornece o seguinte:

-   Uma lista de computadores da rede, que exibe:

    -   O nome do computador

    -   O status do computador, **Online** ou **Offline**

    -   A descrição do computador

    -   O status do backup do computador

    -   O status de atualização do complemento

    -   O status de segurança do computador

    -   O status de alertas do computador

    -   Informações de política de grupo para o computador

-   Um painel de detalhes com informações adicionais sobre um computador selecionado

-   Um painel de tarefas que inclui um conjunto de tarefas administrativas do dispositivo, como exibir alertas e propriedades do computador, configurar o backup do computador e restaurar arquivos e pastas de um backup

#### <a name="to-view-the-status-of-network-computers"></a>Para exibir o status dos computadores da rede

1. Abra o Painel do Windows Server Essentials.

2. Na barra de navegação, clique em **Dispositivos**.

3. Exiba o status de todos os computadores na rede, no painel de lista.

   A tabela a seguir descreve os vários computador e as tarefas de backup que estão disponíveis no Painel do Windows Server Essentials. Algumas tarefas são específicas do computador e são visíveis apenas quando você seleciona um computador na lista.

### <a name="computer-tasks-in-the-dashboard"></a>Tarefas do computador no Painel

|Nome da tarefa|Descrição|
|---------------|-----------------|
|Exibir as propriedades do computador|Exibe informações gerais sobre um computador selecionado e permite exibir detalhes para os backups de computador.|
|Configurar o backup do computador|Executa o Assistente de backup de configuração.|
|Personalizar o backup do computador|Abre as propriedades de backup, das quais você pode fazer alterações nas configurações de backup para o computador selecionado.|
|Iniciar um backup do computador|Inicia um backup de um computador selecionado.|
|Interromper o backup do computador|Interrompe o backup de um computador selecionado.|
|Restaurar arquivos ou pastas para o computador.|Executa o assistente de restauração de arquivos e pastas, permitindo que você restaure unidades, pastas ou arquivos específicos.|
|Exibir alertas para o computador|Exibe críticas e outras alertas informativos e permite que você execute ações corretivas sempre que possível.|
|Área de trabalho remota no computador|Abre a conexão de área de trabalho remota no computador selecionado.|
|Remover o computador|Executa o assistente de remoção de computador, que desliga o computador a partir do Painel do Windows Server Essentials.|
|Personalizar as configurações de backup do computador e histórico de arquivos|Abre a página de configurações de backup, da qual você pode fazer alterações nas configurações de histórico de arquivos e no agendamento de backup para computadores cliente.|
|Como conecto computadores ao servidor?|Abre um tópico da Ajuda que descreve as etapas para executar o ingresso de um computador à rede.|
|Implementar Política de Grupo|Aplica as configurações de política para os computadores Windows 8 e Windows 7 que ingressaram no domínio.|

##  <a name="assign-user-accounts-permission-to-log-on-to-specific-network-computers"></a><a name="BKMK_2"></a> Permissão atribuir contas de usuário para fazer logon em computadores de rede específicos
 Você pode atribuir permissões a contas de usuário para que os usuários possam fazer logon somente em determinados computadores da rede ao acessar a rede do Windows Server Essentials em um local remoto.

#### <a name="to-change-the-computer-access-for-a-user-account"></a>Para alterar o acesso do computador para uma conta de usuário

1.  Abra o Painel do Windows Server Essentials.

2.  Na barra de navegação, clique em **Usuários**.

3.  Na lista de contas de usuário, selecione a conta de usuário que você deseja alterar.

4.  No painel ** \> tarefas da conta de usuário do<** , clique em **exibir as propriedades da conta**. A página **Propriedades** da conta de usuário é exibida.

5.  Na guia **Acesso ao computador**, selecione o computador que o usuário pode acessar remotamente e clique em **OK**.

##  <a name="remove-a-computer-from-the-server"></a><a name="BKMK_3"></a> Remover um computador do servidor
 Quando você remove um computador de um servidor que esteja executando o Windows Server Essentials usando o Painel, ele não é gerenciado pelo servidor. Como resultado, o servidor irá parar de criar backups de computador ou monitorar sua integridade após sua remoção da rede.

> [!NOTE]
>  A remoção de um computador do servidor não desconecte o computador da rede. O computador ainda pode acessar recursos na rede da mesma forma que era possível antes de ser conectado ao servidor. Para impedir que o computador acesse recursos do servidor e para desconectá-lo do servidor, você deve remover o computador do domínio. Além disso, a remoção do computador do servidor não desinstala automaticamente o software Connector ou a barra inicial do computador que está sendo removido. Remova manualmente o software Connector do computador. Para obter mais informações, consulte a seção desinstalar o software do [conector em conectar](../use/Get-Connected-in-Windows-Server-Essentials.md)-se.

#### <a name="to-remove-a-computer-from-the-network-by-using-the-dashboard"></a>Para remover um computador da rede usando o Painel

1.  Abra o Painel do Windows Server Essentials.

2.  Na barra de navegação, clique na guia **Dispositivos**.

3.  Na lista de computadores, clique com o botão direito do mouse no computador que você deseja remover da rede e, em seguida, clique em **Remover o computador**.

##  <a name="configure-group-policy-settings-for-folder-redirection-and-security"></a><a name="BKMK_5"></a> Definir configurações de Política de Grupo para redirecionamento de pasta e segurança
 Você pode configurar a política de grupo e implantá-la em computadores na rede do Windows Server Essentials usando o Painel do Windows Server Essentials. A política de grupo no Windows Server Essentials inclui configurações de redirecionamento de pasta e segurança que influenciam o Windows Update, o Windows Defender e o firewall de rede.

#### <a name="to-configure-group-policy-in-windows-server-essentials"></a>Para configurar a política de grupo no Windows Server Essentials

1.  Abra o Painel do Windows Server Essentials.

2.  Na barra de navegação, clique em **DISPOSITIVOS**.

3.  Para o Windows Server Essentials: no painel **tarefas de usuários** globais, clique em **implementar política de grupo**.

     Para o Windows Server Essentials: no painel **tarefas de dispositivos** globais, clique em **implementar política de grupo**.

4.  O Assistente de Implementação de Política de Grupo é aberto.

5.  Sobre a página **Habilitar a política de grupo de redirecionamento de pasta** do assistente, você pode escolher as pastas de usuário que deseja redirecionar.

6.  Sobre a página **Habilitar configurações de política de segurança** do assistente, você pode optar por habilitar as configurações de política de grupo para o **Windows Update**, o **Windows Defender**e o **Firewall de rede**.

7.  Clique em **Concluir** para implementar as configurações de política de grupo.

##  <a name="connect-to-a-network-computer-by-using-a-remote-desktop-session"></a><a name="BKMK_7"></a> Conectar-se a um computador de rede usando uma sessão de Área de Trabalho Remota
 Para acessar remotamente seu computador de rede do Windows Server Essentials quando você estiver fora do seu escritório, use o navegador da Web para fazer logon no site de Acesso via Web remoto da sua organização e, na guia **computadores** , clique no nome do computador.

 A coluna **Status** mostra se você pode se conectar a um computador na sua rede e se pode incluir os seguintes valores:

-   **Disponível**

     O computador está ligado e está disponível para uma conexão remota. Mesmo se status aparecer, você ainda pode não será capaz de se conectar a esse computador se um firewall de terceiros bloquear a conexão.

-   **Offline ou em espera**

     O computador está desligado ou no modo de suspensão ou de hibernação. Se um computador estiver offline ou em espera, o status é atualizado em tempo real para que você possa saber quando o computador estará disponível.

-   **Sistema operacional sem suporte**

     O sistema operacional no computador não oferece suporte a área de trabalho remota. Pode levar até 6 horas para esse status ser atualizado no servidor, se houver uma alteração.

-   **A conexão está desabilitada**

     A conexão de computador está bloqueada por um firewall ou a área de trabalho remota está desabilitada no computador ou pela política de grupo. Pode levar até 6 horas para esse status ser atualizado no servidor, se houver uma alteração.

##  <a name="view-computer-properties"></a><a name="BKMK_8"></a> Exibir Propriedades do computador
 A seção **Dispositivos** do Painel do Windows Server Essentials exibe uma lista de computadores da rede. A lista também fornece informações adicionais sobre cada computador.

#### <a name="to-view-a-list-of-computers"></a>Para exibir uma lista de computadores

1.  Abra o Painel do Windows Server Essentials.

2.  Na barra de navegação principal, clique em **Dispositivos**.

3.  O Painel exibe uma lista de contas de usuário atual.

#### <a name="to-view-or-change-properties-for-a-computer"></a>Para exibir ou alterar as propriedades de um computador

1.  Na lista de computadores, selecione a conta na qual você deseja exibir ou alterar as propriedades.

2.  No painel ** \> tarefas do<ComputerName** , clique em **exibir as propriedades do computador**. A página **Propriedades** aparecerá para os computadores.

3.  Clique na guia para exibir as propriedades para esse computador.

4.  Para salvar as alterações feitas nas propriedades do computador, clique em **Aplicar**.

## <a name="additional-references"></a>Referências adicionais

-   [Gerenciar o Acesso via Web Remoto](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Usar o Acesso via Web Remoto](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Gerenciar contas de usuário usando o Painel](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)

-   [Gerenciar o Windows Server Essentials](Manage-Windows-Server-Essentials.md)

-   [Utilizar o Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
