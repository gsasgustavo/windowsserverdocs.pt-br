---
title: Etapa 2 – Configurar o WSUS
description: Tópico sobre o WSUS (Windows Server Update Service) – Configurar o WSUS é a etapa dois de um processo de quatro etapas para implantar o WSUS
ms.topic: article
ms.assetid: d4adc568-1f23-49f3-9a54-12a7bec5f27c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 9/18/2020
ms.openlocfilehash: d791151493e98c833a3981d305b81fe0b536b19c
ms.sourcegitcommit: b5c7eaa78e16f3b395611cdbdd4c88dfc653832b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2020
ms.locfileid: "91406279"
---
# <a name="step-2-configure-wsus"></a>Etapa 2: Configurar o WSUS

>Aplica-se a: Windows Server 2019, Windows Server (Canal Semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Depois de instalar a função de servidor do WSUS no servidor, você precisará configurá-lo adequadamente. A lista de verificação a seguir resume as etapas envolvidas ao executar a configuração inicial do servidor do WSUS.

|Tarefa|Descrição|
|----|--------|
|[2.1. Configurar as conexões de rede](#21-configure-network-connections)|Configure a rede de cluster usando o Assistente de Configuração de Rede.|
|[2.2. Configurar o WSUS usando o Assistente de Configuração do WSUS](#22-configure-wsus-by-using-the-wsus-configuration-wizard)|Use o assistente de configuração do WSUS para executar a configuração básica do WSUS.|
|[2.3. Configurar grupos de computadores do WSUS](#23-configure-wsus-computer-groups)|Crie grupos de computadores no console de administração do WSUS para gerenciar atualizações na sua organização.|
|[2.4. Configurar atualizações do cliente](#24-configure-client-updates)|Especifique como e quando as atualizações automáticas são aplicadas aos computadores cliente.|
|[2.5. Proteger o WSUS com o protocolo SSL](#25-secure-wsus-with-the-secure-sockets-layer-protocol)|Configure o protocolo SSL para ajudar a proteger o WSUS (Windows Server Update Services).|

## <a name="21-configure-network-connections"></a>2.1. Configurar as conexões de rede
Para começar o processo de configuração, verifique se sabe as respostas às seguintes perguntas:

1.  O firewall do servidor está configurado para permitir que clientes acessem o servidor?

2.  Este computador pode se conectar ao servidor upstream (como aquele designado para baixar atualizações do Microsoft Update)?

3.  Você tem o nome do servidor proxy e as credenciais do usuário referentes ao servidor proxy, se precisar desses dados?

Por padrão, o WSUS está configurado para usar o Microsoft Update como local de onde serão obtidas as atualizações. Se você tiver um servidor proxy na rede, poderá configurar o WSUS para que use o servidor proxy. Se houver um firewall corporativo entre o WSUS e a Internet, talvez seja necessário configurar o firewall para garantir que o WSUS possa obter atualizações.

> [!TIP]
> Apesar de ser necessária conectividade à Internet para baixar atualizações do Microsoft Update, o WSUS permite importá-las para redes que não está conectadas à Internet.

Quando você tiver as respostas a essas perguntas, poderá começar a configurar as seguintes definições de rede do WSUS:

-   **Atualizações** Especifique a maneira como esse servidor obterá atualizações (no Microsoft Update ou em outro servidor do WSUS).

-   **Proxy** Se você identificou que o WSUS precisa usar um servidor proxy para ter acesso à Internet, configure as definições de proxy no servidor do WSUS.

-   **Firewall** Se você identificou que o WSUS está protegido por um firewall corporativo, há algumas etapas adicionais que precisam ser executadas no dispositivo de borda para permitir adequadamente o tráfego do WSUS.

### <a name="211-connection-from-the-wsus-server-to-the-internet"></a>2.1.1. Conexão do servidor do WSUS com a Internet
Se houver um firewall corporativo entre o WSUS e a Internet, convém configurar o firewall para garantir que o WSUS possa obter atualizações. Para obter atualizações do Microsoft Update, o servidor do WSUS usa a porta 443 para o protocolo HTTPS. Embora a maioria dos firewalls corporativos permita esse tipo de tráfego, algumas empresas restringem o acesso à Internet proveniente dos servidores devido a políticas de segurança internas. Se sua empresa restringir o acesso, você deverá obter autorização para permitir o acesso à Internet via WSUS para a seguinte lista de URLs:

- http\://windowsupdate.microsoft.com

- http\://\*.windowsupdate.microsoft.com

- https\://\*.windowsupdate.microsoft.com

- http\://\*.update.microsoft.com

- https\://\*.update.microsoft.com

- http\://\*.windowsupdate.com

- http\://download.windowsupdate.com

- https\://download.microsoft.com

- http\://\*.download.windowsupdate.com

- http\://wustat.windows.com

- http\://ntservicepack.microsoft.com

- http\://go.microsoft.com

- http\://dl.delivery.mp.microsoft.com

- https\://dl.delivery.mp.microsoft.com

> [!IMPORTANT]
> Para obter um cenário em que o WSUS não consegue obter atualizações devido a configurações de firewall, consulte o [artigo 885819](https://support.microsoft.com/kb/885819) na Base de Dados de Conhecimento Microsoft.

A seção a seguir descreve como configurar um firewall corporativo posicionado entre o WSUS e a Internet. Como o WSUS inicia todo o tráfego de rede, não é necessário configurar o Firewall do Windows no servidor do WSUS. Apesar de a conexão entre o Microsoft Update e o WSUS exigir que as portas 80 e 443 estejam abertas, você pode configurar vários servidores do WSUS para que sejam sincronizadas com uma porta personalizada.

### <a name="212-connection-between-wsus-servers"></a>2.1.2. Conexão entre servidores do WSUS
Os servidores do WSUS upstream e downstream sincronizarão na porta configurada pelo Administrador do WSUS. Por padrão, essas portas são configuradas da seguinte maneira:

-   No WSUS 3.2 e anteriores, a porta 80 para HTTP e 443 para HTTPS

-   No WSUS 6.2 e posterior (pelo menos no Windows Server 2012), as portas 8530 para HTTP e 8531 para HTTPS são usadas

O firewall no servidor do WSUS deve ser configurado para permitir tráfego de entrada nessas portas.

### <a name="213-connection-between-clients-windows-update-agent-and-wsus-servers"></a>2.1.3. Conexão entre clientes (Windows Update Agent) e servidores do WSUS
As portas e interfaces de escuta são configuradas em sites do IIS para o WSUS e em quaisquer configurações de Política de Grupo usadas para configurar PCs cliente. As portas padrão são as mesmas especificadas na seção anterior **Conexão entre servidores do WSUS**e o firewall no servidor do WSUS também deve ser configurado para permitir o tráfego de entrada nessas portas.

## <a name="configure-the-proxy-server"></a>Configurar o servidor proxy
Se a rede corporativa usar servidores proxy, eles devem dar suporte aos protocolos HTTP e SSL e usar a autenticação básica ou a autenticação do Windows. Esses requisitos podem ser atendidos usando uma das seguintes configurações:

1.  Um servidor proxy único que dá suporte a dois canais de protocolo. Nesse caso, defina um canal para usar HTTP e o outro canal para usar HTTPS.

    > [!NOTE]
    > Você pode configurar um servidor proxy que lida com ambos os protocolos do WSUS durante a instalação do software de servidor do WSUS.

2.  Dois servidores proxy, cada um deles dá suporte a um único protocolo. Nesse caso, um servidor proxy é configurado para usar HTTP e o outro servidor proxy é configurado para usar HTTPS.

Para configurar dois servidores proxy, cada um dos quais lidará com um protocolo para o WSUS, use o procedimento a seguir:

#### <a name="to-set-up-wsus-to-use-two-proxy-servers"></a>Para configurar o WSUS para usar dois servidores proxy

1.  Faça logon no computador que deve ser o servidor do WSUS usando uma conta que seja membro do grupo de Administradores local.

2.  Instale a função de servidor do WSUS Durante o Assistente de Configuração do WSUS (discutido na próxima seção) não especifique um servidor proxy.

3.  Abra um prompt de comando (Cmd.exe) como um administrador. Para abrir um prompt de comando como administrador, acesse **Iniciar**. Em **Iniciar pesquisa**, digite **Prompt de comando**. Na parte superior do menu Iniciar, clique com o botão direito do mouse no **Prompt de comando** e, em seguida, clique em **Executar como administrador**. Se a caixa de diálogo **Controle de Conta de Usuário** for exibida, insira as credenciais adequadas (se solicitado), confirme se a ação exibida é o que você deseja e, em seguida, clique em **Continuar**.

4.  Na janela do Prompt de comando, vá para a pasta C:\Arquivos de Programas\Update Services\Tools. Digite o seguinte comando:

    **wsusutil ConfigureSSlproxy [< proxy_server proxy_port>] -enable**, em que:

    1.  proxy_server é o nome do servidor proxy que dá suporte ao HTTPS.

    2.  proxy_port é o número da porta do servidor proxy.

5.  Feche a janela do Prompt de comando.

Para adicionar o servidor proxy que usa o protocolo HTTP à configuração do WSUS, use o procedimento a seguir:

#### <a name="to-add-a-proxy-server-that-uses-the-http-protocol"></a>Para adicionar um servidor proxy que usa o protocolo HTTP

1.  Abra o Console de Administração do WSUS.

2.  No painel esquerdo, expanda o nome do servidor e, em seguida, clique em **Opções**.

3.  No painel **Opções** , clique em **Origem da Atualização e Servidor de Atualização**e clique na guia **Servidor Proxy** .

4.  Use as opções a seguir para modificar a configuração do servidor proxy existente:

    ###### <a name="to-change-or-add-a-proxy-server-to-the-wsus-configuration"></a>Para alterar ou adicionar um servidor proxy na configuração do WSUS

    1.  Marque a caixa de seleção de **Utilizar um servidor proxy ao sincronizar**.

    2.  Na caixa de texto **Nome do Servidor Proxy** , digite o nome do servidor proxy.

    3.  Na caixa de texto **Número da Porta Proxy** , digite o número da porta do servidor proxy O número da porta padrão é 80.

    4.  Se o servidor proxy exigir que você use uma conta de usuário específica, selecione a caixa de seleção **Usar credenciais de usuário para se conectar ao servidor proxy**. Digite o nome de usuário, o domínio e a senha necessários nas caixas de texto correspondentes.

    5.  Se o servidor proxy der suporte à autenticação básica, marque a caixa de seleção **Permitir autenticação básica (a senha é enviada em texto não criptografado)** .

    6.  Clique em **OK**.

    ###### <a name="to-remove-a-proxy-server-from-the-wsus-configuration"></a>Para remover um servidor proxy da configuração do WSUS

    1.  Para remover um servidor proxy da configuração do WSUS, desmarque a caixa de seleção de **Utilizar um servidor proxy ao sincronizar**.

    2.  Clique em **OK**.

## <a name="22-configure-wsus-by-using-the-wsus-configuration-wizard"></a>2.2. Configurar o WSUS usando o Assistente de Configuração do WSUS
Este procedimento pressupõe que você esteja usando o Assistente de Configuração do WSUS, que aparece na primeira vez em que você inicia o Console de Gerenciamento do WSUS. Mais adiante neste tópico, você saberá como executar essas configurações usando a página **Opções** :

#### <a name="to-configure-wsus"></a>Para configurar o WSUS

1.  No painel de navegação do Gerenciador do Servidor, clique em **Painel**, clique em **Ferramentas**e clique em **Windows Server Update Services**.

    > [!NOTE]
    > Se a caixa de diálogo **Concluir a instalação do WSUS** aparecer, clique em **Executar**. Na caixa de diálogo **Concluir a instalação do WSUS**, clique em **Fechar** quando a instalação for concluída com êxito.

2.  O Assistente do Windows Server Update Services é aberto. Na página **Antes de Começar** , analise a informação e clique em **Avançar**.

3.  Leia as instruções na página **Ingressar no Programa de Aperfeiçoamento do Microsoft Update** e avalie se quer participar. Se você deseja participar do programa. Mantenha a seleção padrão ou desmarque a caixa de seleção e, em seguida, clique em **Avançar**.

4.  Na página **Escolher Servidor Upstream** , há duas opções:

    1.  Sincronizar as atualizações com o Microsoft Update

    2.  Sincronizar de outro servidor do Windows Server Update Services

        -   Se você optar por sincronizar de outro servidor do WSUS, especifique o nome do servidor e a porta em que ele se comunicará com o servidor upstream.

        -   Para usar SSL, marque a caixa de seleção **Usar SSL ao sincronizar informações de atualização** . Os servidores usarão a porta 443 para sincronização. (Verifique se esse servidor e o servidor upstream dão suporte a SSL).

        -   Se esse for um servidor de réplica, marque a caixa de seleção **Esta é uma réplica do servidor upstream**.

5.  Depois de selecionar as opções adequadas para sua implantação, clique em **Avançar** para continuar.

6.  Na página **Especificar Servidor Proxy** , marque a caixa de seleção **Utilizar um servidor proxy ao sincronizar** e digite o nome do servidor proxy e o número da porta (porta 80, por padrão) nas caixas correspondentes.

    > [!IMPORTANT]
    > Você precisa concluir essa etapa se identificou que o WSUS precisa de um servidor proxy para ter acesso à Internet.

7.  Se quiser se conectar ao servidor proxy usando credenciais de usuário específicas, marque a caixa de seleção **Utilize credenciais de usuário para se conectar ao servidor proxy** e digite o nome de usuário, o domínio e a senha nas caixas correspondentes. Se quiser habilitar autenticação básica para o usuário que está se conectando ao servidor proxy, marque a caixa de seleção **Permitir autenticação básica (a senha é enviada em texto não criptografado)** .

8.  Clique em **Avançar**. Na página **Conectar ao Servidor Upstream**, clique em **Iniciar conexão**.

9. Quando a conexão for estabelecida, clique em **Avançar** para continuar.

10. Na página **Escolher Idiomas**, você tem a opção de escolher os idiomas em que o WSUS receberá atualizações — todos os idiomas ou um subconjunto de idiomas. A seleção de um subconjunto de idiomas fará economizar espaço em disco, mas é IMPORTANTE escolher todos os idiomas necessários a todos os clientes desse servidor do WSUS. Se você optar por obter atualizações somente para idiomas específicos, escolha **Baixar atualizações somente nestes idiomas** e escolha os idiomas para os quais deseja atualizações; caso contrário, deixe a seleção padrão.

    > [!WARNING]
    > Se você escolher a opção **Baixar atualizações somente nestes idiomas**e este servidor tiver um servidor downstream do WSUS conectado a ele, essa opção forçará o servidor downstream a também usar somente os idiomas escolhidos.

11. Depois de selecionar as opções de idioma adequadas para sua implantação, clique em **Avançar** para continuar.

12. A página **Escolher Produtos** permite especificar os produtos para os quais você deseja atualizações. Escolha as categorias de produtos, como Windows, ou produtos específicos, como Windows Server 2008. A seleção de uma categoria de produtos abrange todos os produtos dessa categoria.

13. Selecione as opções de produto adequadas para sua implantação e clique em **Avançar**.

14. Na página **Escolher Classificações** , escolha as classificações de atualização que deseja obter. Escolha todas as classificações ou um subconjunto delas e clique em **Avançar**.

15. A página **Definir Agenda de Sincronização** permite que você selecione se executará a sincronização em modo manual ou automático.

    -   Se você escolher **Sincronizar manualmente**, inicie o processo de sincronização pelo Console de Administração do WSUS.

    -   Se você escolher **Sincronizar automaticamente**, o servidor do WSUS será sincronizado em intervalos definidos.

    Defina o tempo para a **Primeira sincronização**e especifique o número de **Sincronizações por dia** que deseja que este servidor execute. Por exemplo, se você especificar que deve haver quatro sincronizações por dia, começando às 3h00, as sincronizações ocorrerão às 3h00, 9h00, 15h00 e 21h00.

16. Depois de selecionar as opções de sincronização adequadas para sua implantação, clique em **Avançar** para continuar.

17. Na página **Concluído** , você tem a opção de começar a sincronização imediatamente marcando a caixa de seleção **Começar a sincronização inicial** . Se você não escolher essa opção, será necessário usar o Console de Gerenciamento do WSUS para executar a sincronização inicial. Clique em **Avançar** se quiser ler mais sobre configurações adicionais ou clique em **Concluir** para concluir este assistente e a configuração inicial do WSUS.

18. Depois de clicar em **Concluir**, será exibido o Console de Gerenciamento do WSUS.

Agora que você executou a configuração básica do WSUS, leia as próximas seções para saber mais detalhes sobre como alterar as configurações usando o Console de Gerenciamento do WSUS.

## <a name="23-configure-wsus-computer-groups"></a>2.3. Configurar grupos de computadores do WSUS
Os grupos de computadores são uma parte IMPORTANTE das implantações do WSUS (Windows Server Update Services). Os grupos de computadores permitem testar e direcionar atualizações para computadores específicos. Há dois grupos de computadores padrão: Todos os computadores e Computadores não atribuídos. Por padrão, quando cada computador cliente contata pela primeira vez o servidor do WSUS, o servidor adiciona esse computador cliente a ambos os grupos.

Você pode criar quantos grupos de computadores personalizados precisar para gerenciar atualizações em sua organização. Como prática recomendada, crie pelo menos um grupo de computadores para testar as atualizações antes de implantá-las em outros computadores de sua organização.

Use o procedimento a seguir para criar um novo grupo e atribuir um computador a esse grupo:

#### <a name="to-create-a-computer-group"></a>Para criar um grupo de computadores

1.  No Console de Administração do WSUS, em **Update Services**, expanda o servidor do WSUS, expanda **Computadores**, clique com o botão direito do mouse em **Todos os computadores** e clique em **Adicionar grupo de computadores**.

2.  Na caixa de diálogo **Adicionar grupo de computadores**, em **Nome**, especifique o nome do novo grupo e clique em **Adicionar**.

3.  Clique em **Computadores** e escolha os computadores que quer atribuir a esse novo grupo.

4.  Clique com o botão direito do mouse nos nomes dos computadores escolhidos na etapa anterior e clique em **Alterar associação**.

5.  Na caixa de diálogo **Definir associação a um grupo de computadores**, escolha o grupo de teste que você criou e clique em **OK**.

## <a name="24-configure-client-updates"></a>2.4. Configurar atualizações do cliente
A Instalação do WSUS configura automaticamente o IIS para que distribua a versão mais recente das Atualizações Automáticas a cada computador cliente que contata o servidor do WSUS. A melhor maneira de configurar as Atualizações Automáticas depende do ambiente de rede.

-   Em um ambiente que usa o serviço de diretório Active Directory, você pode usar um GPO (Objeto de Política de Grupo) baseado em domínio existente ou criar um novo GPO.

-   Em um ambiente sem Active Directory, use o Editor de Política de Grupo Local para configurar as Atualizações Automáticas e aponte os computadores cliente para o servidor do WSUS.

> [!IMPORTANT]
> Os procedimentos a seguir pressupõem que a rede execute o Active Directory. Esses procedimentos também pressupõem que você tem familiaridade com Política de Grupo e a use para gerenciar a rede.

Use os procedimentos a seguir para configurar as Atualizações Automáticas para computadores clientes:

-   [Etapa 4: Definir as configurações da Política de Grupo para atualizações automáticas](4-configure-group-policy-settings-for-automatic-updates.md)

-   [2.3. Configurar grupos de computadores](#23-configure-wsus-computer-groups) neste tópico

### <a name="configure-automatic-updates-in-group-policy"></a>Configurar Atualizações Automáticas na Política de Grupo

Se você tiver configurado o Active Directory na rede, poderá configurar um ou vários computadores simultaneamente incluindo-os em um GPO (Objeto de Política de Grupo) e configurando esse GPO com as definições do WSUS. É recomendável criar um novo GPO que contenha somente as definições do WSUS.

Vincule esse GPO do WSUS a um contêiner do Active Directory que seja apropriado para o seu ambiente. Em um ambiente simples, você pode vincular um único GPO do WSUS ao domínio. Em um ambiente mais complexo, você pode vincular vários GPOs do WSUS a várias OUs (unidades organizacionais), que permitirão aplicar diferentes definições de política do WSUS a diferentes tipos de computadores.

##### <a name="to-enable-wsus-through-a-domain-gpo"></a>Para habilitar o WSUS por meio de um GPO de domínio

1.  No GPMC (Console de Gerenciamento de Política de Grupo), navegue até o GPO em que deseja configurar o WSUS e clique em **Editar**.

2.  No GPMC, expanda **Configuração do Computador**, expanda **Políticas**, expanda **Modelos Administrativos**, expanda **Componentes do Windows** e clique em **Windows Update**.

3.  No painel de detalhes, clique duas vezes em **Configurar Atualizações Automáticas**. A política **Configurar Atualizações Automáticas** é aberta.

4.  Clique em **Habilitado**e selecione uma das opções a seguir na definição **Configurar atualização automática** :

    -   **Avisar antes de baixar e de instalar qualquer atualização**. Esta opção notifica um usuário administrativo conectado antes de baixar e instalar as atualizações.

    -   **Baixar automaticamente e notificar antes de instalar**. Esta opção começa automaticamente a baixar as atualizações e notifica um usuário administrativo conectado antes de instalá-las. Por padrão, essa opção é selecionada.

    -   **Baixar automaticamente e agendar a instalação**. Esta opção começa automaticamente a baixar as atualizações e as instala no dia e hora que você especificar.

    -   **Permitir que o administrador local escolha a configuração**. Esta opção permite que administradores locais usem as Atualizações Automáticas do Painel de Controle para escolher uma opção de configuração. Por exemplo, eles podem optar por agendar uma instalação. Os administradores locais não podem desabilitar as Atualizações Automáticas.

5.  Selecione **Habilitar destino do lado do cliente**, selecione **Habilitado** e, em seguida, digite o nome do grupo de computadores do WSUS ao qual você deseja adicionar este computador na caixa **Nome do grupo de destino para este computador**.

    > [!NOTE]
    > **Habilitar destino do lado do cliente** permite que os computadores cliente se adicionem aos grupos de computadores de destino no servidor do WSUS quando as Atualizações Automáticas são redirecionadas para um servidor do WSUS. Se o status for definido como Habilitado, este computador se identificará como um membro de um determinado grupo de computadores quando ele envia informações para o servidor do WSUS, que as utiliza para determinar quais atualizações estão implantadas no computador. Essa configuração indica ao servidor do WSUS qual grupo o computador cliente usará. Você deve criar o grupo no servidor do WSUS e adicionar computadores membros do domínio ao grupo.

6.  Clique em **OK** para fechar a política **Habilitar destino do lado do cliente** e retornar ao painel de detalhes do Windows Update.

7.  Clique em **OK** para fechar a política **Configurar Atualizações Automáticas** e retornar ao painel de detalhes do Windows Update.

8.  No painel de detalhes do **Windows Update** , clique duas vezes em **Especificar o local do serviço de atualização na intranet da Microsoft**.

9. Clique em **Habilitado**e, em seguida, no servidor nas caixas de texto **Definir o serviço intranet de atualização para detectar atualizações** e **Definir o servidor de estatísticas da intranet** Por exemplo, digite *http://servername* em ambas as caixas (em que *servername* é o nome do servidor do WSUS).

    > [!WARNING]
    > Ao digitar o endereço da intranet do servidor do WSUS, verifique se especificou qual porta será usada. Por padrão, o WSUS usará a porta 8530 para HTTP, e 8531 para HTTPS. Por exemplo, se você estiver usando HTTP, deverá digitar **http://servername:8530** .

10. Clique em **OK**.

Depois de configurar um computador cliente, levará algum tempo até que o computador apareça na página **Computadores** no Console de Administração do WSUS. Para computadores clientes que estão configurados com um Objeto de Política de Grupo baseado em domínio, pode levar cerca de 20 minutos para que a Política de Grupo aplique as novas definições de política ao computador cliente. Por padrão, a Política de Grupo é atualizada em segundo plano a cada 90 minutos, com um deslocamento aleatório de 0 a 30 minutos. Se você quiser atualizar uma Política de Grupo antes em tempo menor, pode abrir uma janela Prompt de comando no computador cliente e digitar gpupdate /force.

Para computadores cliente que estão configurados usando o editor de Política de Grupo Local, o GPO é aplicado imediatamente e a atualização leva cerca de 20 minutos. Se você começar a detecção manualmente, não precisará aguardar 20 minutos para que o computador cliente contate o WSUS.

Como a espera para que a detecção comece pode ser um processo demorado, você pode usar o seguinte procedimento para iniciá-la imediatamente.

##### <a name="to-initiate-wsus-detection"></a>Para iniciar uma detecção do WSUS

1.  No computador cliente, abra uma janela Prompt de comando com privilégios elevados.

2.  Digite wuauclt.exe /detectnow e pressione ENTER.

## <a name="25-secure-wsus-with-the-secure-sockets-layer-protocol"></a>2.5. Proteger o WSUS com o protocolo SSL

Você pode usar o protocolo SSL para ajudar a proteger a implantação do WSUS. O WSUS usa o SSL para autenticar computadores cliente e servidores de WSUS downstream para o servidor do WSUS. Além disso, o WSUS usa SSL para criptografar metadados de atualização.

> [!IMPORTANT]
> Os clientes e servidores downstream que estão configurados para usar a TLS (Segurança da Camada de Transporte) ou HTTPS também devem ser configurados para usar um FQDN (nome de domínio totalmente qualificado) para o servidor do WSUS upstream.

O WSUS usa SSL apenas para metadados, não para arquivos de atualização. Essa é a mesma forma que o Microsoft Update distribui as atualizações. A Microsoft reduz o risco de enviar arquivos de atualização por um canal não criptografado assinando cada atualização. Além disso, um hash é calculado e enviado junto com os metadados para cada atualização. Quando uma atualização é baixada, o WSUS verifica a assinatura digital e o hash. Se a atualização tiver sido alterada, ela não é instalada.

### <a name="limitations-of-wsus-ssl-deployments"></a>Limitações das implantações de SSL do WSUS
Você deve considerar as seguintes limitações ao usar SSL para proteger uma implantação do WSUS:

1.  O uso de SSL aumenta a carga de trabalho do servidor. Você deve esperar uma queda de 10% do desempenho devido ao custo de criptografar todos os metadados que são enviados pela rede.

2.  Se você usar o WSUS com um banco de dados SQL Server remoto, a conexão entre o servidor do WSUS e o servidor de banco de dados não é protegida por SSL. Se a conexão de banco de dados deve ser protegida, considere as seguintes recomendações:

-   Mova o banco de dados do WSUS para o servidor do WSUS.

-   Mova o servidor de banco de dados remoto e o servidor do WSUS para uma rede privada.

-   Implante o IPsec (Segurança de Protocolo IP) para ajudar a proteger o tráfego de rede. Para obter mais informações sobre IPsec, consulte [Criando e usando políticas IPSec](https://go.microsoft.com/fwlink/?LinkID=203841).

### <a name="configure-ssl-on-the-wsus-server"></a>Configurar o SSL no servidor do WSUS
O WSUS requer duas portas para o SSL: uma porta que usa HTTPS para enviar metadados criptografados e uma porta que usa HTTP para enviar atualizações. Ao configurar o WSUS para usar SSL, considere o seguinte:

-   Você não pode configurar o site inteiro do WSUS para exigir SSL porque todo o tráfego para o site do WSUS precisa ser criptografado. O WSUS criptografa apenas os metadados de atualização. Se um computador tentar recuperar arquivos de atualização na porta HTTPS, a transferência falhará.

    Você deve exigir o SSL apenas para as seguintes raízes virtuais:

    -   **SimpleAuthWebService**

    -   **DSSAuthWebService**

    -   **ServerSyncWebService**

    -   **APIremoting30**

    -   **ClientWebService**

    Você não deve exigir o SSL para as seguintes raízes virtuais:

    -   **Conteúdo**

    -   **Inventário**

    -   **ReportingWebService**

    -   **SelfUpdate**

-   O certificado da AC (autoridade de certificação) deve ser importado para o repositório de AC raiz confiável do computador local ou o repositório de AC raiz confiável do Windows Server Update Service em servidores do WSUS downstream. Se o certificado foi importado apenas para o repositório de AC raiz confiável do usuário local, o servidor do WSUS downstream não será autenticado no servidor upstream.

    Para obter mais informações sobre como usar os certificados SSL no IIS, confira [Exigir o protocolo SSL (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=203846).

-   Você deve importar o certificado para todos os computadores que se comunicarão com o servidor do WSUS. Isso inclui todos os computadores cliente, servidores downstream e computadores que executam o Console de Administração do WSUS. O certificado deve ser importado para o repositório de AC raiz confiável do computador local ou para o repositório de AC raiz confiável do Windows Server Update Service.

-   Você pode usar qualquer porta para o SSL. No entanto, a porta que você configurar para o SSL também determina a porta que o WSUS usa para enviar o tráfego HTTP não criptografado. Considere os seguintes exemplos:

    -   Se você usar a porta padrão do setor 443 para o tráfego HTTPS, o WSUS usará a porta padrão do setor 80 para o tráfego HTTP não criptografado.

    -   Se você usar qualquer porta diferente de 443 para o tráfego HTTPS, o WSUS enviará o tráfego HTTP não criptografado pela porta que numericamente vem antes da porta para HTTPS. Por exemplo, se você usar a porta 8531 para HTTPS, o WSUS usará porta 8530 para HTTP.

-   Você deve reiniciar o *ClientServicingProxy* se o nome do servidor, a configuração de SSL ou o número da porta for alterado.

##### <a name="to-configure-ssl-on-the-wsus-root-server"></a>Para configurar o SSL no servidor raiz do WSUS

1.  Faça logon no servidor do WSUS usando uma conta que seja membro do grupo de Administradores do WSUS ou do grupo de Administradores local.

2.  Acesse **Iniciar**, digite **CMD**, clique com o botão direito do mouse em **Prompt de comando** e clique em **Executar como administrador**.

3.  Navegue até a pasta _%ProgramFiles%_ **\\Serviços de Atualização\\Ferramentas\\** .

4.  Na janela Prompt de comando, digite o seguinte comando:

    **Wsusutil configuressl**_certificateName_

    onde:

    *certificateName* é o nome DNS do servidor do WSUS.

### <a name="configure-ssl-on-client-computers"></a>Configurar o SSL em computadores cliente
Ao configurar o SSL em computadores cliente, você deve considerar as seguintes questões:

-   Você deve incluir uma URL para uma porta segura no servidor do WSUS. Como você não pode exigir o SSL no servidor, a única maneira de garantir que os computadores cliente podem usar um canal de segurança é usando uma URL que especifica o HTTPS. Se usar qualquer porta diferente de 443 para SSL, você também deverá incluir essa porta na URL.

-   O certificado em um computador cliente deve ser importado para o repositório de AC raiz confiável do computador local ou no repositório de AC raiz confiável do Serviço de Atualização Automática. Se o certificado for importado apenas para o repositório do AC raiz confiável do usuário local, as Atualizações Automáticas apresentarão falha na autenticação do servidor.

-   Os computadores cliente devem confiar no certificado que você associar ao servidor do WSUS. Dependendo do tipo de certificado usado, você precisará configurar um serviço para habilitar os computadores cliente para confiarem no certificado vinculado ao servidor do WSUS.

### <a name="configure-ssl-for-downstream-wsus-servers"></a>Configurar o SSL para servidores do WSUS downstream
As instruções a seguir configuram um servidor downstream para sincronizar com um servidor upstream que usa o SSL.

##### <a name="to-synchronize-a-downstream-server-to-an-upstream-server-that-uses-ssl"></a>Para sincronizar um servidor downstream para um servidor upstream que usa o SSL

1.  Faça logon no computador usando uma conta de usuário que seja membro do grupo de Administradores local ou do grupo de Administradores do WSUS.

2.  Clique em **Iniciar**, em **Todos os Programas**, em **Ferramentas Administrativas** e, em seguida, em **Windows Server Update Services**.

3.  No painel direito, expanda o nome do servidor.

4.  Clique em **Opções**e em **Origem da Atualização e Servidor Proxy**.

5.  Na página **Origem da Atualização** , selecione **Sincronizar de outro servidor do Windows Server Update Services**.

6.  Digite o nome do servidor upstream na caixa de texto **Nome do servidor**. Digite o número da porta usada pelo servidor para conexões SSL na caixa de texto **Número da porta**.

7.  Marque a caixa de seleção **Usar SSL ao sincronizar informações de atualização** e clique em **OK**.

### <a name="additional-ssl-resources"></a>Recursos adicionais do SSL
As etapas necessárias para configurar uma autoridade de certificação, associe o certificado ao site do WSUS e estabelecer uma relação de confiança entre os computadores cliente e o certificado estão além do escopo deste guia. Para obter mais informações e instruções sobre como instalar certificados e configurar esse ambiente, consulte os seguintes tópicos:

-   [Guia passo a passo de PKI do Suite B](https://go.microsoft.com/fwlink/?LinkID=203858)

-   [Como implementar e administrar modelos de certificado](https://go.microsoft.com/fwlink/?LinkID=203859)

-   [Guia de atualização e migração dos Serviços de Certificados do Active Directory](https://go.microsoft.com/fwlink/?LinkID=203860)

-   [Configurar o registro automático de certificado](https://go.microsoft.com/fwlink/?LinkID=203861)

### <a name="26-complete-iis-configuration"></a>2.6. Concluir a configuração de IIS
Por padrão, o acesso de leitura anônimo está habilitado para site padrão e todos os novos sites do IIS. Alguns aplicativos, principalmente o Windows SharePoint Services, podem remover o acesso anônimo. Se isso tiver ocorrido, você deverá reabilitar o acesso de leitura anônimo antes de ser possível instalar e operar o WSUS com êxito.

Para habilitar o acesso de leitura anônimo, siga as etapas para a versão aplicável do IIS:

1.  [Habilitar autenticação Anônima (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=205316), conforme documentado no Guia de Operações do IIS 7.

2.  [Habilitando a autenticação anônima (IIS 6.0)](https://go.microsoft.com/fwlink/?LinkId=211391), conforme documentado no Guia de Operações do IIS 6.0.

### <a name="27-configure-a-signing-certificate"></a>2.7. Configurar um certificado de assinatura
O WSUS tem a capacidade de publicar pacotes de atualização personalizada para atualizar produtos Microsoft e não Microsoft. O WSUS pode assinar esses pacotes de atualização personalizada automaticamente para você com um certificado Authenticode. Para habilitar a assinatura de atualização personalizada, você deve instalar um certificado de assinatura de pacote no seu servidor do WSUS. Há várias considerações associadas à assinatura de atualização personalizada.

1.  **Distribuição de certificados**. A chave privada deve ser instalada no servidor do WSUS e a chave pública deve ser explicitamente instalada no repositório de certificados confiáveis em todos os servidores e PCs cliente que devem receber atualizações assinadas personalizadas.

2.  **Expiração** Quando o certificado autoassinado expirar ou se aproximar da expiração, o WSUS registrará os eventos no log de eventos.

3.  **Atualizações/revogação de certificados**. Se você desejava atualizar ou revogar um certificado (ou seja, depois de descobrir que ele expirou), o WSUS não oferecia nenhuma funcionalidade para habilitar essa opção. Fazer isso se tornou uma tarefa manual que era muito difícil fazer manualmente ou de automatizar com êxito.


