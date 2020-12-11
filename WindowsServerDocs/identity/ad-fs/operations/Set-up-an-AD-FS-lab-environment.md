---
description: 'Saiba mais sobre: configurar um ambiente de laboratório de AD FS'
ms.assetid: 276a7f7d-5faa-4c00-a51c-3fa511fe52f9
title: Configurar um ambiente de laboratório do AD FS
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 0b7c4c40ea37c9d8f7f2e7dd5639245a98a25aab
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039684"
---
# <a name="set-up-an-ad-fs-lab-environment"></a>Configurar um ambiente de laboratório do AD FS

Este tópico destaca as etapas para configurar um ambiente de teste que pode ser usado para concluir as etapas dos seguintes guias passo a passo:

-   [Passo a passo: Ingressar no Local de Trabalho com um dispositivo iOS](Walkthrough--Workplace-Join-with-an-iOS-Device.md)

-   [Passo a passo: Ingressar no local de trabalho com um dispositivo do Windows](Walkthrough--Workplace-Join-with-a-Windows-Device.md)

-   [Guia passo a passo: Gerenciar risco com o Controle de Acesso Condicional](Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)

-   [Guia de instruções: gerenciar riscos com autenticação multifator adicional para aplicativos confidenciais](Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

> [!NOTE]
> Não é recomendável instalar o servidor Web e o servidor de federação no mesmo computador.

Para configurar esse ambiente de teste, conclua as seguintes etapas:

1.  [Etapa 1: Configurar o controlador de domínio (DC1)](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_1)

2.  [Etapa 2: configurar o servidor de Federação (ADFS1) com o serviço de registro de dispositivo](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)

3.  [Etapa 3: Configurar o servidor Web (WebServ1) e um aplicativo de amostra baseado em declarações](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_5)

4.  [Etapa 4: Configurar o computador cliente (Client1)](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_10)

## <a name="step-1-configure-the-domain-controller-dc1"></a><a name="BKMK_1"></a>Etapa 1: Configurar o controlador de domínio (DC1)
Para os fins deste ambiente de teste, você pode chamar a raiz Active Directory domínio **contoso.com** e especificar <strong>pass@word1</strong> como a senha de administrador.

-   Instale o serviço de função AD DS e instale Active Directory Domain Services (AD DS) para tornar o computador um controlador de domínio no Windows Server 2012 R2. Esta ação atualiza o esquema de AD DS como parte da criação do controlador de domínio. Para obter mais informações e instruções passo a passo, consulte[ https://technet.microsoft.com/ library/hh472162. aspx](../../ad-ds/deploy/install-active-directory-domain-services--level-100-.md).

### <a name="create-test-active-directory-accounts"></a><a name="BKMK_2"></a>Criar contas de teste do Active Directory
Depois que o controlador de domínio estiver funcionando, você poderá criar contas de grupo de teste e de usuário de teste no domínio e adicionar a conta de usuário à conta de grupo. Essas contas são usadas para concluir as etapas dos guias passo a passo que foram citados anteriormente neste tópico.

Crie as seguintes contas:

- Usuário: **Robert Hatley** com as seguintes credenciais: nome de usuário: **RobertH** e senha: <strong>P@ssword</strong>

- Grupo: **Finance**

Para obter informações sobre como criar contas de usuário e de grupo no Active Directory (AD), consulte [https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx](/previous-versions/windows/it-pro/windows-server-2003/cc783323(v=ws.10)) .

Adicione a conta **Robert Hatley** ao grupo **Finance**. Para obter informações sobre como adicionar um usuário a um grupo no Active Directory, consulte [https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx](/previous-versions/windows/it-pro/windows-server-2003/cc737130(v=ws.10)) .

### <a name="create-a-gmsa-account"></a>Criar uma conta GMSA
A conta de conta de serviço gerenciado de grupo (GMSA) é necessária durante a instalação e configuração do Serviços de Federação do Active Directory (AD FS) (AD FS).

##### <a name="to-create-a-gmsa-account"></a>Para criar uma conta GMSA

1.  Abra uma janela de comando do Windows PowerShell e digite:

    ```
    Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)
    New-ADServiceAccount FsGmsa -DNSHostName adfs1.contoso.com -ServicePrincipalNames http/adfs1.contoso.com

    ```

## <a name="step-2-configure-the-federation-server-adfs1-by-using-device-registration-service"></a><a name="BKMK_4"></a>Etapa 2: Configurar o servidor de federação (ADFS1) usando o Device Registration Service
Para configurar outra máquina virtual, instale o Windows Server 2012 R2 e conecte-o ao domínio **contoso.com**. Configure o computador depois de tê-lo associado ao domínio e, em seguida, vá para instalar e configurar a função de AD FS.

Veja o vídeo de instruções [Serviços de Federação do Active Directory: instalando um farm de servidores AD FS](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search).

### <a name="install-a-server-ssl-certificate"></a>Instalar um certificado SSL de servidor
Você deve instalar um certificado SSL (Secure Socket Layer) no servidor ADFS1, no repositório do computador local. O certificado DEVE ter os seguintes atributos:

-   Nome da Entidade (CN): adfs1.contoso.com

-   Nome Alternativo da Entidade (DNS): adfs1.contoso.com

-   Nome Alternativo da Entidade (DNS): enterpriseregistration.contoso.com

[Diretrizes de Serviço Web de Registro de Certificado](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831822(v=ws.11)#configure-a-ca-for-the-certificate-enrollment-web-service)

[Vídeo de instruções do Serviços de Federação do Active Directory: atualizando certificados](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search).

### <a name="install-the-ad-fs-server-role"></a>Instalar a função de servidor AD FS

##### <a name="to-install-the-federation-service-role-service"></a>Para instalar o serviço de função Serviço de Federação

1. Faça logon no servidor usando a conta de administrador de domínio administrator@contoso.com .

2. Inicie o Gerenciador do Servidor. Para iniciar o Gerenciador do Servidor, clique em **Gerenciador do Servidor** na tela **Iniciar** do Windows ou clique em **Gerenciador do Servidor** na barra de tarefas do Windows, na área de trabalho do Windows. Na guia **Início Rápido** do bloco **Bem-vindo** da página **Painel**, clique em **Adicionar funções e recursos**. Opcionalmente, você pode clicar em **Adicionar Funções e Recursos** no menu **Gerenciar**.

3. Na página **Antes de começar** , clique em **Avançar**.

4. Na página **Selecionar tipo de instalação**, clique em **Instalação baseada em função ou recurso** e em **Avançar**.

5. Na página **Selecionar servidor de destino**, clique em **Selecionar um servidor no pool de servidor**, verifique se o computador de destino está selecionado e clique em **Avançar**.

6. Na página **Selecionar funções do servidor**, clique em **Serviços de Federação do Active Directory** e, depois, clique em **Avançar**.

7. Na página **Selecionar recursos**, clique em **Avançar**.

8. Na página **Serviço de Federação do Active Directory (AD FS)**, clique em **Avançar**.

9. Após ter verificado as informações na página **Confirmar as seleções de instalação**, marque a caixa de seleção **Reiniciar o servidor de destino automaticamente se for necessário**, e em seguida clique em **Instalar**.

10. Na página **Progresso da instalação**, verifique se tudo está instalado corretamente e, depois, clique em **Fechar**.

### <a name="configure-the-federation-server"></a>Configurar o servidor de federação
A próxima etapa é configurar o servidor de federação.

##### <a name="to-configure-the-federation-server"></a>Para configurar o servidor de federação

1.  Na página **Painel** do do Gerenciador do Servidores, clique no sinalizador **Notificações** e, em seguida, clique em **Configurar o serviço de federação no servidor**.

    O **Assistente de Configuração do Serviço de Federação do Active Directory** é aberto.

2.  Na página **Bem-vindo**, selecione **Criar o primeiro servidor de federação em um farm de servidores de federação** e clique em **Avançar**.

3.  Na página **Conectar ao AD DS**, especifique uma conta com direitos de administrador de domínio para o domínio **contoso.com** do Active Directory no qual esse computador ingressou e clique em **Avançar**.

4.  Na página **Especificar Propriedades de Serviço**, siga estas etapas e clique em **Avançar**:

    -   Importe o certificado SSL que você obteve anteriormente. Esse é o certificado obrigatório de autenticação de serviço. Navegue até o local do seu certificado SSL.

    -   Para especificar um nome para o serviço de federação, digite **adfs1.contoso.com**. Esse valor é o mesmo fornecido quando você registrou um certificado SSL no AD CS (Serviços de Certificados do Active Directory).

    -   Para especificar um nome de exibição para seu serviço de federação, digite **Contoso Corporation**.

5.  Na página **Especificar Conta de Serviço**, selecione **Use uma Conta de Serviço Gerenciado de grupo ou de conta de usuário de domínio existente** e especifique a conta GMSA **fsgmsa** criada quando você criou o controlador de domínio.

6.  Na página **Especificar Banco de Dados de Configuração**, selecione **Crie um banco de dados neste servidor que utiliza o Banco de Dados Interno do Windows** e clique em **Avançar**.

7.  Na página **Examinar Opções**, verifique suas seleções de configuração e clique em **Avançar**.

8.  Na página **Verificações de Pré-requisitos**, certifique-se de que todas as verificações de pré-requisitos tenham sido concluídas com sucesso e clique em **Configurar**.

9. Na página **Resultados**, examine os resultados, verifique se a configuração foi concluída com sucesso e clique em **As próximas etapas são necessárias para concluir a implantação do serviço de federação**.

### <a name="configure-device-registration-service"></a>Configurar o Device Registration Service
A próxima etapa é configurar o Device Registration Service no servidor ADFS1. Veja o vídeo de instruções [Serviços de Federação do Active Directory: habilitando o Device Registration Service](https://channel9.msdn.com/).

##### <a name="to-configure-device-registration-service-for-windows-server-2012-rtm"></a>Para configurar o Device Registration Service para o Windows Server 2012 RTM

1.  > [!IMPORTANT]
    > **As etapas a seguir se aplicam à compilação RTM do Windows Server 2012 R2.**

    Abra uma janela de comando do Windows PowerShell e digite:

    ```
    Initialize-ADDeviceRegistration
    ```

    Quando for solicitada uma conta de serviço, digite **contosofsgmsa $**.

    Agora, execute o cmdlet do Windows PowerShell.

    ```
    Enable-AdfsDeviceRegistration
    ```

2.  No servidor ADFS1, no console **Gerenciamento do AD FS**, navegue para **Políticas de Autenticação**. Selecione **Editar Autenticação Primária Global**. Marque a caixa de seleção ao lado de **Habilitar Autenticação de Dispositivo** e clique em **OK**.

### <a name="add-host-a-and-alias-cname-resource-records-to-dns"></a>Adicionar registros de recurso de host (A) e alias (CNAME) ao DNS
No DC1, você deve assegurar que os seguintes registros DNS (Sistema de Nomes de Domínio) sejam criados para o Device Registration Service.

|Entrada|Tipo|Endereço|
|---------|--------|-----------|
|adfs1|Host (A)|Endereço IP do servidor de AD FS|
|enterpriseregistration|Alias (CNAME)|adfs1.contoso.com|

Você pode usar o procedimento a seguir para adicionar um registro de recurso de host (A) aos servidores de nome DNS corporativos para o servidor de federação e Device Registration Service.

A associação no grupo Administradores ou equivalente é o requisito mínimo para concluir esse procedimento. Examine os detalhes sobre como usar as contas apropriadas e as associações de grupo no hiperlink " <https://go.microsoft.com/fwlink/?LinkId=83477> " grupos padrão de domínio e local ( <https://go.microsoft.com/fwlink/p/?LinkId=83477> ).

##### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>Para adicionar registros de recursos de host (A) e alias (CNAME) ao DNS do seu servidor de federação

1.  No DC1, no Gerenciador do Servidor, no menu **Ferramentas**, clique em **DNS** para abrir o snap-in DNS.

2.  Na árvore de console, expanda DC1, expanda **Zonas de Pesquisa Direta**, clique com o botão direito do mouse em **contoso.com** e clique em **Novo Host (A ou AAAA)**.

3.  Em **Nome**, digite o nome que deseja usar para seu farm do AD FS. Para este passo a passo, digite **adfs1**.

4.  Em **Endereço IP**, digite o endereço IP do servidor ADFS1. Clique em **Adicionar Host**.

5.  Clique com o botão direito do mouse em **contoso.com** e clique em **Novo Alias (CNAME)**.

6.  Na caixa de diálogo **Novo Registro de Recurso**, digite **enterpriseregistration** na caixa **Nome do alias**.

7.  Na caixa FQDN (Nome de Domínio Totalmente Qualificado) do host de destino, digite **adfs1.contoso.com** e clique em **OK**.

    > [!IMPORTANT]
    > Em uma implantação real, se sua empresa tiver vários sufixos UPN, você deverá criar vários registros CNAME, um para cada sufixo UPN no DNS.

## <a name="step-3-configure-the-web-server-webserv1-and-a-sample-claims-based-application"></a><a name="BKMK_5"></a>Etapa 3: Configurar o servidor Web (WebServ1) e um aplicativo de amostra baseado em declarações
Configure uma máquina virtual (WebServ1) instalando o sistema operacional Windows Server 2012 R2 e conecte-o ao domínio **contoso.com**. Depois do ingresso no domínio, você pode prosseguir para instalar e configurar a função Servidor Web.

Para concluir os guias passo a passo citados anteriormente neste tópico, você deve ter um aplicativo de amostra que esteja protegido pelo seu servidor de federação (ADFS1).

Você pode baixar o SDK do Windows Identity Foundation ( [https://www.microsoft.com/download/details.aspx?id=4451](https://www.microsoft.com/download/details.aspx?id=4451) , que inclui um aplicativo de exemplo baseado em declarações.

Você deve concluir as etapas a seguir para configurar um servidor Web com esse aplicativo de amostra baseado em declarações.

> [!NOTE]
> Essas etapas foram testadas em um servidor Web que executa o sistema operacional Windows Server 2012 R2.

1.  [Instalar a função de servidor Web e o Windows Identity Foundation](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_15)

2.  [Instalar o SDK do Windows Identity Foundation](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_13)

3.  [Configurar o aplicativo de declarações simples em IIS](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_9)

4.  [Criar um objeto de confiança de terceira parte confiável no servidor de federação](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_11)

### <a name="install-the-web-server-role-and-windows-identity-foundation"></a><a name="BKMK_15"></a>Instalar a função Servidor Web e o Windows Identity Foundation

1. > [!NOTE]
   > Você deve ter acesso à mídia de instalação do Windows Server 2012 R2.

   Faça logon no WebServ1 usando <strong>administrator@contoso.com</strong> o e a senha <strong>pass@word1</strong> .

2. No Gerenciador do Servidor, na guia **Início Rápido** do bloco **Bem-vindo** da página **Painel**, clique em **Adicionar funções e recursos**. Opcionalmente, você pode clicar em **Adicionar Funções e Recursos** no menu **Gerenciar**.

3. Na página **Antes de começar** , clique em **Avançar**.

4. Na página **Selecionar tipo de instalação**, clique em **Instalação baseada em função ou recurso** e em **Avançar**.

5. Na página **Selecionar servidor de destino**, clique em **Selecionar um servidor no pool de servidor**, verifique se o computador de destino está selecionado e clique em **Avançar**.

6. Na página **Selecionar funções de servidor**, marque a caixa de seleção ao lado de **Servidor Web (IIS)**, clique em **Adicionar Recursos** e, depois, em **Avançar**.

7. Na página **Selecionar recursos**, selecione **Windows Identity Foundation 3.5** e clique em **Avançar**.

8. Na página **Função de Servidor Web (IIS)**, clique em **Avançar**.

9. Na página **Selecionar serviços de função**, selecione e expanda **Desenvolvimento de Aplicativo**. Selecione **ASP.NET 3.5**, clique em **Adicionar Recursos** e, então, em **Avançar**.

10. Na página **Confirmar seleções de instalação**, clique em **Especificar um caminho de origem alternativo**. Insira o caminho para o diretório SxS localizado na mídia de instalação do Windows Server 2012 R2. Por exemplo, D:SourcesSxs. Clique em **OK** e em **Instalar**.

### <a name="install-windows-identity-foundation-sdk"></a><a name="BKMK_13"></a>Instalar o SDK do Windows Identity Foundation

1.  Execute WindowsIdentityFoundation-SDK-3.5.msi para instalar o SDK 3,5 do Windows Identity Foundation ( https://www.microsoft.com/download/details.aspx?id=4451) . Escolha todas as opções padrão.

### <a name="configure-the-simple-claims-app-in-iis"></a><a name="BKMK_9"></a>Configurar o aplicativo de declarações simples em IIS

1.  Instale um certificado SSL válido no repositório de certificados do computador. O certificado deve conter o nome do seu servidor Web: **webserv1.contoso.com**.

2.  Copie o conteúdo de arquivos C:Program (x86) Windows Identity Foundation SDKv 3.5 SamplesQuick StartWeb ApplicationPassiveRedirectBasedClaimsAwareWebApp para C:InetpubClaimapp.

3.  Edite o arquivo **Default.aspx.cs** para que não ocorra nenhuma filtragem de declaração. Essa etapa é realizada para garantir que o aplicativo de amostra exiba todas as declarações que são emitidas pelo servidor de federação. Faça o seguinte:

    1.  Abra **Default.aspx.cs** em um editor de texto.

    2.  Pesquise o arquivo na segunda instância de `ExpectedClaims`.

    3.  Comente toda a instrução `IF` e suas chaves. Indique comentários digitando "//" (sem as aspas) no início de uma linha.

    4.  Agora sua instrução `FOREACH` deve ser semelhante a este código de exemplo.

        ```
        Foreach (claim claim in claimsIdentity.Claims)
        {
           //Before showing the claims validate that this is an expected claim
           //If it is not in the expected claims list then don't show it
           //if (ExpectedClaims.Contains( claim.ClaimType ) )
           // {
              writeClaim( claim, table );
           //}
        }

        ```

    5.  Salve e feche **Default.aspx.cs**.

    6.  Abra **web.config** em um editor de texto.

    7.  Remova toda a seção `<microsoft.identityModel>` . Remova tudo começando em `including <microsoft.identityModel>` até e inclusive `</microsoft.identityModel>`.

    8.  Salve e feche **web.config**.

4.  **Configurar o Gerenciador do IIS**

    1.  Abra o **Gerenciador do IIS (Serviços de Informações da Internet)** .

    2.  Vá para **Pools de Aplicativos** e clique com o botão direito do mouse em **DefaultAppPool** para selecionar **Configurações Avançadas**. Defina **Carregar Perfil do Usuário** como **Verdadeiro** e clique em **OK**.

    3.  Clique com o botão direito do mouse em **DefaultAppPool** para selecionar **Configurações Básicas**. Altere a **Versão do CLR .NET** para a **Versão do CLR .NET v2.0.50727**.

    4.  Clique com o botão direito do mouse em **Site Padrão** para selecionar **Editar Associações**.

    5.  Adicione uma associação **HTTPS** à porta **443** com o certificado SSL que você tem instalado.

    6.  Clique com o botão direito do mouse em **Site Padrão** para selecionar **Adicionar Aplicativo**.

    7.  Defina o alias como **ClaimApp** e o caminho físico como **c:inetpubclaimapp**.

5.  Para configurar **claimapp** para que funcione com o servidor de federação, faça o seguinte:

    1.  Execute FedUtil.exe, localizado em **arquivos C:Program (x86) Windows Identity Foundation sdkv 3.5**.

    2.  Defina o local de configuração do aplicativo como **C:inetputclaimappweb.config** e defina o URI do aplicativo como a URL do seu site, **https://webserv1.contoso.com /ClaimApp/**. Clique em **Avançar**.

    3.  Selecione **usar um STS existente** e navegue até a URL de metadados do AD FS Server **https://adfs1.contoso.com/federationmetadata/2007-06/federationmetadata.xml** . Clique em **Avançar**.

    4.  Selecione **Desabilitar validação da cadeia de certificados** e clique em **Avançar**.

    5.  Selecione **Sem criptografia** e clique em **Avançar**. Na página **Solicitações oferecidas**, clique em **Avançar**.

    6.  Marque a caixa de seleção ao lado de **Agendar uma tarefa para realizar atualizações diárias de metadados de WS-Federation**. Clique em **Concluir**.

    7.  Seu aplicativo de amostra está configurado. Se você testar a URL do aplicativo **https://webserv1.contoso.com/claimapp** , ele deverá redirecioná-lo para o servidor de Federação. O servidor de federação deve exibir uma página de erro porque você ainda não configurou o objeto de confiança de terceira parte confiável. Em outras palavras, você não protegeu este aplicativo de teste por AD FS.

Agora você deve proteger seu aplicativo de exemplo que é executado em seu servidor Web com AD FS. Para isso, adicione um objeto de confiança de terceira parte confiável ao servidor de federação (ADFS1). Veja o [Vídeo de instruções dos Serviços de Federação do Active Directory: adicionar um objeto de confiança de terceira parte confiável](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search).

### <a name="create-a-relying-party-trust-on-your-federation-server"></a><a name="BKMK_11"></a>Criar um objeto de confiança de terceira parte confiável no servidor de federação

1.  No servidor de federação (ADFS1), no console **Gerenciamento do AD FS**, navegue para **Objetos de Confiança de Terceira Parte Confiável** e clique em **Adicionar Objeto de Confiança de Terceira Parte Confiável**.

2.  Na página **Selecionar Fonte de Dados**, selecione **Importar dados sobre a terceira parte confiável publicados online ou em um local da rede**, digite a URL dos metadados de **claimapp** e clique em **Avançar**. A execução de FedUtil.exe criou um arquivo .xml de metadados. Ele está localizado em **https://webserv1.contoso.com/claimapp/federationmetadata/2007-06/federationmetadata.xml** .

3.  Na página **Especificar Nome de Exibição**, especifique o **nome de exibição** do objeto de confiança de terceira parte confiável (**claimapp**) e clique em **Avançar**.

4.  Na página **Configurar Multi-Factor Authentication Agora?**, selecione **Não desejo especificar a configuração de autenticação de vários fatores para esse objeto de confiança de terceira parte confiável no momento** e clique em **Avançar**.

5.  Na página **Escolher Regras de Autorização de Emissão**, selecione **Permitir que todos os usuários acessem esta terceira parte confiável** e clique em **Avançar**.

6.  Na página **Pronto para Adicionar Objeto de Confiança**, clique em **Avançar**.

7.  Na caixa de diálogo **Editar Regras de Declaração**, clique em **Adicionar Regra**.

8.  Na página **Escolher Tipo de Regra**, selecione **Enviar Declarações Usando uma Regra Personalizada** e clique em **Avançar**.

9. Na página **Configurar Regra de Declaração**, na caixa **Nome da regra de declaração**, digite **All Claims**. Na caixa **Regra personalizada**, digite a seguinte regra de declaração.

    ```
    c:[ ]
    => issue(claim = c);

    ```

10. Clique em **Concluir** e em **OK**.

## <a name="step-4-configure-the-client-computer-client1"></a><a name="BKMK_10"></a>Etapa 4: Configurar o computador cliente (Client1)
Configure outra máquina virtual e instale Windows 8.1. Essa máquina virtual deve estar na mesma rede virtual das outras máquinas. Esse computador NÃO deve ingressar no domínio Contoso.

O cliente DEVE confiar no certificado SSL usado para o servidor de federação (ADFS1) configurado na [Step 2: Configure the federation server (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4). Ele também deve ser capaz de validar informações de revogação do certificado.

Você também deve configurar e usar uma conta da Microsoft para fazer logon no Client1.

## <a name="see-also"></a>Consulte Também
[Serviços de Federação do Active Directory (AD FS) How-To série de vídeos: instalando um farm](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search) 
 de servidores AD FS [Serviços de Federação do Active Directory (AD FS) How-To série de vídeo: Atualizando certificados](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search) 
 [Serviços de Federação do Active Directory (AD FS) How-To série de vídeos: adicionar uma terceira parte confiável](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search) 
 [Série de vídeo do Serviços de Federação do Active Directory (AD FS) How-To: Habilitando o serviço](https://channel9.msdn.com/) 
 de registro do dispositivo [Serviços de Federação do Active Directory (AD FS) How-To série de vídeos: Instalando o proxy de aplicativo Web](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search)

