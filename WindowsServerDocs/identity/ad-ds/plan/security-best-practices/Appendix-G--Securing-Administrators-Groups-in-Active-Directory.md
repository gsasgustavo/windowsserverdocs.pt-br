---
description: 'Saiba mais sobre: Apêndice G: protegendo grupos de administradores no Active Directory'
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: Apêndice G-protegendo grupos de administradores no Active Directory
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 93ddd6cf87b3736895b15ff185e43dc0e98da78c
ms.sourcegitcommit: 3247e193d9fe1b57543fff215460a6d9db52f58b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/30/2020
ms.locfileid: "97815025"
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>Apêndice G: Proteger grupos de administradores no Active Directory

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>Apêndice G: Proteger grupos de administradores no Active Directory
Como é o caso dos grupos Enterprise Admins (EA) e admins. do domínio (DA), a associação no grupo Administradores internos (BA) deve ser necessária apenas em cenários de compilação ou recuperação de desastres. Não deve haver contas de usuário do dia a dia no grupo Administradores, com exceção da conta interna de administrador para o domínio, se ele tiver sido protegido, conforme descrito no [Apêndice D: protegendo Built-In contas de administrador no Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).

Os administradores são, por padrão, os proprietários da maioria dos objetos AD DS em seus respectivos domínios. A associação a esse grupo pode ser necessária em cenários de compilação ou recuperação de desastres nos quais a propriedade ou a capacidade de apropriar-se de objetos é necessária. Além disso, o DAs e EAs herdam vários direitos e permissões em virtude de sua associação padrão no grupo Administradores. O aninhamento de grupo padrão para grupos com privilégios no Active Directory não deve ser modificado, e o grupo de administradores de cada domínio deve ser protegido conforme descrito nas instruções passo a passo a seguir.

Para o grupo Administradores em cada domínio na floresta:

1.  Remova todos os membros do grupo Administradores, com a possível exceção da conta de administrador interno para o domínio, desde que ele tenha sido protegido, conforme descrito no [Apêndice D: Protegendo contas de administrador de Built-In no Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).

2.  Em GPOs vinculados a UOs que contêm servidores membros e estações de trabalho em cada domínio, o grupo BA deve ser adicionado aos seguintes direitos de usuário em Computer \ Diretivas \ \ **políticas \ Atribuição de direitos de usuário**:

    -   Negar acesso a este computador pela rede

    -   Negar o logon como um trabalho em lotes

    -   Negar o logon como um serviço

3.  Na UO Controladores de domínio em cada domínio na floresta, o grupo Administradores deve receber os seguintes direitos de usuário:

    -   Acesso a este computador da rede

    -   Permitir logon localmente

    -   Permitir logon por meio dos Serviços de Área de Trabalho Remota

4.  A auditoria deve ser configurada para enviar alertas se qualquer modificação for feita nas propriedades ou na associação do grupo Administradores.

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>Instruções passo a passo para remover todos os membros do grupo de administradores

1.  Em **Gerenciador do servidor**, clique em **ferramentas** e em **Active Directory usuários e computadores**.

2.  Para remover todos os membros do grupo Administradores, execute as seguintes etapas:

    1.  Clique duas vezes no grupo **Administradores** e clique na guia **Membros** .

        ![Captura de tela que mostra a guia Membros para remover todos os membros do grupo Administradores.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)

    2.  Selecione um membro do grupo, clique em **remover**, em **Sim** e em **OK**.

3.  Repita a etapa 2 até que todos os membros do grupo Administradores tenham sido removidos.

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>Instruções detalhadas para proteger grupos de administradores no Active Directory

1.  Em **Gerenciador do servidor**, clique em **ferramentas** e clique em **Gerenciamento de política de grupo**.

2.  Na árvore de console, expanda &lt; floresta &gt; \Domains \\ &lt; domínio &gt; e, em seguida, **política de grupo objetos** (em que &lt; floresta &gt; é o nome da floresta e &lt; domínio &gt; é o nome do domínio no qual você deseja definir o política de grupo).

3.  Na árvore de console, clique com o botão direito do mouse em **política de grupo objetos** e clique em **novo**.

    ![Captura de tela que mostra onde selecionar novo para que você possa proteger grupos de administradores no Active Directory.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)

4.  Na caixa de diálogo **novo GPO** , digite <GPO Name> e clique em **OK** (em que *nome do GPO* é o nome desse GPO).

    ![Captura de tela que mostra onde nomear a G P O na caixa de diálogo novo GPO para que você possa proteger os grupos de administradores.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)

5.  No painel de detalhes, clique com o botão direito do mouse **<GPO Name>** e clique em **Editar**.

6.  Navegue até **computador \ \ Diretivas**\ \ políticas e clique em **atribuição de direitos de usuário**.

    ![Captura de tela que mostra onde navegar para que você possa selecionar a opção de administrador de direitos de usuário para proteger os grupos de administradores.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)

7.  Configure os direitos de usuário para impedir que os membros do grupo administradores acessem servidores membros e estações de trabalho na rede fazendo o seguinte:

    1.  Clique duas vezes em **negar acesso a este computador da rede** e selecione **definir estas configurações de política**.

    2.  Clique em **Adicionar usuário ou grupo** e clique em **procurar**.

    3.  Digite **Administradores**, clique em **verificar nomes** e clique em **OK**.

        ![Captura de tela que mostra como verificar se você configurou os direitos de usuário para impedir que os membros do grupo administradores acessem servidores membros e estações de trabalho na rede.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)

    4.  Clique em **OK** e em **OK** novamente.

8.  Configure os direitos de usuário para impedir que os membros do grupo Administradores façam logon como um trabalho em lotes fazendo o seguinte:

    1.  Clique duas vezes em **Negar logon como um trabalho em lotes** e selecione **definir estas configurações de política**.

    2.  Clique em **Adicionar usuário ou grupo** e clique em **procurar**.

    3.  Digite **Administradores**, clique em **verificar nomes** e clique em **OK**.

        ![Captura de tela que mostra como verificar se você configurou os direitos de usuário para impedir que os membros do grupo administradores efetuem logon como um trabalho em lotes.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)

    4.  Clique em **OK** e em **OK** novamente.

9. Configure os direitos de usuário para impedir que os membros do grupo Administradores façam logon como um serviço fazendo o seguinte:

    1.  Clique duas vezes em **Negar logon como um serviço** e selecione **definir estas configurações de política**.

    2.  Clique em **Adicionar usuário ou grupo** e clique em **procurar**.

    3.  Digite **Administradores**, clique em **verificar nomes** e clique em **OK**.

        ![Captura de tela que mostra como verificar se você configurou os direitos de usuário para impedir que os membros do grupo administradores efetuem logon como um serviço.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)

    4.  Clique em **OK** e em **OK** novamente.

10. Para sair **Editor de gerenciamento de política de grupo**, clique em **arquivo** e em **sair**.

11. No **Gerenciamento de política de grupo**, VINCULE o GPO ao servidor membro e às UOs de estação de trabalho fazendo o seguinte:

    1.  Navegue até a &lt; floresta &gt;> \\ &lt; domínio \Domains &gt; (em que &lt; floresta &gt; é o nome da floresta e &lt; domínio &gt; é o nome do domínio no qual você deseja definir a política de grupo).

    2.  Clique com o botão direito do mouse na UO à qual o GPO será aplicado e clique em **vincular um GPO existente**.

        ![Captura de tela que mostra o link de uma opção de menu G P O existente quando você clica com o botão direito do mouse na UO.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)

    3.  Selecione o GPO que você acabou de criar e clique em **OK**.

        ![Captura de tela que mostra onde selecionar o GPO que você acabou de criar.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)

    4.  Crie links para todas as outras UOs que contêm estações de trabalho.

    5.  Crie links para todas as outras UOs que contêm servidores membro.

        > [!IMPORTANT]
        > Se os servidores de salto forem usados para administrar controladores de domínio e Active Directory, verifique se os servidores de salto estão localizados em uma UO à qual esses GPOs não estão vinculados.

        > [!NOTE]
        > Quando você implementa restrições no grupo Administradores em GPOs, o Windows aplica as configurações aos membros do grupo de administradores locais de um computador, além do grupo de administradores do domínio. Portanto, você deve ter cuidado ao implementar restrições no grupo Administradores. Embora seja recomendável proibir logons de rede, lote e serviço para membros do grupo Administradores, sempre que for viável implementá-los, não restringir logons locais ou logons por meio de Serviços de Área de Trabalho Remota. O bloqueio desses tipos de logon pode bloquear a administração legítima de um computador por membros do grupo local de administradores.
        >
        > A captura de tela a seguir mostra as definições de configuração que bloqueiam o uso indevido de contas internas de administrador de domínio e locais, além do uso indevido de grupos internos de administradores de domínio ou locais. Observe que o direito de usuário **Negar logon pelo serviços de área de trabalho remota** não inclui o grupo Administradores, pois incluí-lo nessa configuração também bloquearia esses logons para contas que são membros do grupo Administradores do computador local. Se os serviços em computadores estiverem configurados para serem executados no contexto de qualquer um dos grupos privilegiados descritos nesta seção, a implementação dessas configurações poderá fazer com que os serviços e aplicativos falhem. Portanto, assim como todas as recomendações nesta seção, você deve testar exaustivamente as configurações de aplicabilidade em seu ambiente.

        ![Captura de tela que mostra as definições de configuração que bloqueiam o uso indevido de contas internas de administrador de domínio e locais.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>Instruções passo a passo para conceder direitos de usuário ao grupo de administradores

1.  Em **Gerenciador do servidor**, clique em **ferramentas** e clique em **Gerenciamento de política de grupo**.

2.  Na árvore de console, expanda <Forest> \Domains \\ <Domain> e, em seguida, **política de grupo objetos** (em que <Forest> é o nome da floresta e <Domain> é o nome do domínio no qual você deseja definir o política de grupo).

3.  Na árvore de console, clique com o botão direito do mouse em **política de grupo objetos** e clique em **novo**.

    ![Captura de tela que mostra o menu exibido quando você clica com o botão direito do mouse em objetos de Política de Grupo.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)

4.  Na caixa de diálogo **novo GPO** , digite <GPO Name> e clique em **OK** (em que <GPO Name> é o nome desse GPO).

    ![Captura de tela que mostra onde nomear o G P O para que você possa proteger os grupos de administradores.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)

5.  No painel de detalhes, clique com o botão direito do mouse **<GPO Name>** e clique em **Editar**.

6.  Navegue até **computador \ \ Diretivas**\ \ políticas e clique em **atribuição de direitos de usuário**.

    ![Captura de tela que mostra onde navegar para que você possa selecionar administrador de direitos de usuário para proteger grupos de administradores.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)

7.  Configure os direitos de usuário para permitir que os membros do grupo administradores acessem os controladores de domínio pela rede fazendo o seguinte:

    1.  Clique duas vezes em **acesso a este computador da rede** e selecione **definir estas configurações de política**.

    2.  Clique em **Adicionar usuário ou grupo** e clique em **procurar**.

    3.  Clique em **Adicionar usuário ou grupo** e clique em **procurar**.

        ![Captura de tela que mostra como verificar se você configurou os direitos de usuário para permitir que os membros do grupo administradores acessem os controladores de domínio pela rede.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)

    4.  Clique em **OK** e em **OK** novamente.

8.  Configure os direitos de usuário para permitir que os membros do grupo Administradores façam logon localmente fazendo o seguinte:

    1.  Clique duas vezes em **Permitir logon localmente** e selecione **definir estas configurações de política**.

    2.  Clique em **Adicionar usuário ou grupo** e clique em **procurar**.

    3.  Digite **Administradores**, clique em verificar **nomes** e clique em **OK**.

        ![Captura de tela que mostra como verificar se você configurou os direitos de usuário para permitir que os membros do grupo Administradores façam logon localmente.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)

    4.  Clique em **OK** e em **OK** novamente.

9. Configure os direitos de usuário para permitir que os membros do grupo Administradores façam logon por meio de Serviços de Área de Trabalho Remota fazendo o seguinte:

    1.  Clique duas vezes em **Permitir logon por meio de serviços de área de trabalho remota** e selecione **definir estas configurações de política**.

    2.  Clique em **Adicionar usuário ou grupo** e clique em **procurar**.

    3.  Digite **Administradores**, clique em **verificar nomes** e clique em **OK**.

        ![Captura de tela que mostra como verificar se você configurou os direitos de usuário para permitir que os membros do grupo Administradores façam logon por meio de Serviços de Área de Trabalho Remota.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)

    4.  Clique em **OK** e em **OK** novamente.

10. Para sair **Editor de gerenciamento de política de grupo**, clique em **arquivo** e em **sair**.

11. No **Gerenciamento de política de grupo**, VINCULE o GPO à UO Controladores de domínio fazendo o seguinte:

    1.  Navegue até <Forest> \Domains \\ <Domain> (em que <Forest> é o nome da floresta e <Domain> é o nome do domínio no qual você deseja definir a política de grupo).

    2.  Clique com o botão direito do mouse na UO Controladores de domínio e clique em **vincular um GPO existente**.

        ![Captura de tela que mostra a opção vincular um menu de GPO existente quando você está tentando vincular a G P o à UO Controladores de domínio.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)

    3.  Selecione o GPO que você acabou de criar e clique em **OK**.

        ![Captura de tela que mostra onde selecionar o GPO que você acabou de criar enquanto estiver vinculando o G P O para as estações de trabalho e o servidor do membro.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)

#### <a name="verification-steps"></a>Etapas de Verificação

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Verificar as configurações de GPO "negar acesso a este computador pela rede"
De qualquer servidor membro ou estação de trabalho que não seja afetada pelas alterações de GPO (como um "servidor de salto"), tente acessar um servidor membro ou estação de trabalho na rede que é afetada pelas alterações de GPO. Para verificar as configurações do GPO, tente mapear a unidade do sistema usando o comando **net use** .

1.  Faça logon localmente usando uma conta que seja membro do grupo Administradores.

2.  Com o mouse, mova o ponteiro para o canto superior direito ou inferior direito da tela. Quando a **barra** de botões for exibida, clique em **Pesquisar**.

3.  Na caixa de **pesquisa** , digite **prompt de comando**, clique com o botão direito do mouse em prompt de **comando** e clique em **Executar como administrador** para abrir um prompt de comando com privilégios elevados.

4.  Quando for solicitado a aprovar a elevação, clique em **Sim**.

    ![Captura de tela que realça a caixa de diálogo controle de conta de usuário.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)

5.  Na janela do **prompt de comando** , digite **net use \\ \\ \<Server Name\> \c $**, em que \<Server Name\> é o nome do servidor membro ou da estação de trabalho que você está tentando acessar pela rede.

6.  A captura de tela a seguir mostra a mensagem de erro que deve aparecer.

    ![Captura de tela que realça a mensagem de erro de falha de logon.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Verificar as configurações de GPO "Negar logon como um trabalho em lotes"
De qualquer servidor membro ou estação de trabalho afetada pelas alterações do GPO, faça logon localmente.

###### <a name="create-a-batch-file"></a>Criar um arquivo em lotes

1.  Com o mouse, mova o ponteiro para o canto superior direito ou inferior direito da tela. Quando a **barra** de botões for exibida, clique em **Pesquisar**.

2.  Na caixa de **pesquisa** , digite **bloco de notas** e clique em **bloco de notas**.

3.  No **bloco de notas**, digite **dir c:**.

4.  Clique em **arquivo** e em **salvar como**.

5.  No campo **nome do arquivo** , digite **<Filename> . bat** (em que <Filename> é o nome do novo arquivo em lotes).

###### <a name="schedule-a-task"></a>Agendar uma tarefa

1.  Com o mouse, mova o ponteiro para o canto superior direito ou inferior direito da tela. Quando a **barra** de botões for exibida, clique em **Pesquisar**.

2.  Na caixa de **pesquisa** , digite **Agendador de tarefas** e clique em **Agendador de tarefas**.

    > [!NOTE]
    > Em computadores que executam o Windows 8, na caixa de pesquisa, digite agendar tarefas e clique em agendar tarefas.

3.  Clique em **ação** e clique em **criar tarefa**.

4.  Na caixa de diálogo **criar tarefa** , digite **<Task Name>** (em que <Task Name> é o nome da nova tarefa).

5.  Clique na guia **ações** e clique em **novo**.

6.  No campo **ação** , selecione **Iniciar um programa**.

7.  No campo **programa/script** , clique em **procurar**, localize e selecione o arquivo em lotes criado na seção **criar um arquivo em lotes** e clique em **abrir**.

8.  Clique em **OK**.

9. Clique na guia **Geral**.

10. No campo **Opções de segurança** , clique em **Alterar usuário ou grupo**.

11. Digite o nome de uma conta que seja membro do grupo Administradores, clique em **verificar nomes** e clique em **OK**.

12. Selecione **executar se o usuário estiver conectado ou não** e não **armazenar a senha**. A tarefa só terá acesso aos recursos do computador local.

13. Clique em **OK**.

14. Uma caixa de diálogo deve ser exibida, solicitando credenciais de conta de usuário para executar a tarefa.

15. Depois de inserir a senha, clique em **OK**.

16. Uma caixa de diálogo semelhante à seguinte deve aparecer.

    ![Captura de tela que realça a caixa de diálogo Agendador de Tarefas.](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Verificar as configurações de GPO "Negar logon como um serviço"

1.  De qualquer servidor membro ou estação de trabalho afetada pelas alterações do GPO, faça logon localmente.

2.  Com o mouse, mova o ponteiro para o canto superior direito ou inferior direito da tela. Quando a **barra** de botões for exibida, clique em **Pesquisar**.

3.  Na caixa de **pesquisa** , digite **Serviços** e clique em **Serviços**.

4.  Localize e clique duas vezes em **spooler de impressão**.

5.  Clique na guia **Logon**.

6.  No campo **fazer logon como** , selecione **esta conta**.

7.  Clique em **procurar**, digite o nome de uma conta que seja membro do grupo Administradores, clique em **verificar nomes** e clique em **OK**.

8.  Nos campos **senha** e **Confirmar senha** , digite a senha da conta selecionada e clique em **OK**.

9. Clique em **OK** mais três vezes.

10. Clique com o botão direito do mouse em **spooler de impressão** e clique em **reiniciar**.

11. Quando o serviço for reiniciado, uma caixa de diálogo semelhante à seguinte deverá ser exibida.

    ![proteger grupos de administradores](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Reverter alterações para o serviço spooler de impressora

1.  De qualquer servidor membro ou estação de trabalho afetada pelas alterações do GPO, faça logon localmente.

2.  Com o mouse, mova o ponteiro para o canto superior direito ou inferior direito da tela. Quando a **barra** de botões for exibida, clique em **Pesquisar**.

3.  Na caixa de **pesquisa** , digite **Serviços** e clique em **Serviços**.

4.  Localize e clique duas vezes em **spooler de impressão**.

5.  Clique na guia **Logon**.

6.  No campo **fazer logon como** , clique em conta **sistema local** e clique em **OK**.
