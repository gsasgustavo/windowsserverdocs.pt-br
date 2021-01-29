---
description: Crie um aplicativo do lado do servidor que usa clientes confidenciais OAuth. Use AD FS 2016 ou posterior.
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: Criar um aplicativo do lado do servidor que usa clientes confidenciais do OAuth usando o Serviços de Federação do Active Directory (AD FS) 2016 ou posterior
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: 2302d8fd1d6d00943316a62578d1d8d9ee096169
ms.sourcegitcommit: d1815253b47e776fb96a3e91556fd231bef8ee6d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2021
ms.locfileid: "99042572"
---
# <a name="build-a-server-side-app-that-uses-oauth-confidential-clients-by-using-ad-fs-2016-or-later"></a>Criar um aplicativo do lado do servidor que usa clientes confidenciais do OAuth usando o AD FS 2016 ou posterior


O Serviços de Federação do Active Directory (AD FS) (AD FS) 2016 e posteriores dá suporte a clientes que podem manter seu próprio segredo, como um aplicativo ou serviço executado em um servidor Web.  Esses clientes são conhecidos como *clientes confidenciais*.

Este artigo descreve um aplicativo Web em execução em um servidor Web. O aplicativo serve como um cliente confidencial para AD FS.

## <a name="prerequisites"></a>Pré-requisitos
Você precisará dos seguintes recursos: 

-   Ferramentas de cliente do GitHub.

-   AD FS no Windows Server 2016 Technical Preview 4 ou posterior. (Este artigo pressupõe que AD FS foi instalado.)

-   Visual Studio 2013 ou posterior.

## <a name="create-an-application-group"></a>Criar um grupo de aplicativos

Para criar um grupo de aplicativos no AD FS 2016 ou posterior:

1.  Em gerenciamento de AD FS, clique com o botão direito do mouse em **grupos de aplicativos**. Em seguida, selecione **Adicionar grupo de aplicativos**.

2.  No **Assistente para Adicionar grupo de aplicativos**: 
    1. Em **nome**, insira *ADFSOAUTHCC*. 
    1. Em **aplicativos cliente-servidor**, selecione o **aplicativo de servidor acessando um modelo de API Web** .  
    1. Selecione **Avançar**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG" alt-text="Captura de tela que mostra onde selecionar o modelo para o aplicativo de servidor que acessa uma P e r." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG":::

3.  Copie o valor do **identificador de cliente** . Você o usará posteriormente no arquivo de *web.config* do aplicativo. É o valor para `ida:ClientId` .

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG" alt-text="Captura de tela que mostra onde copiar o valor do identificador de cliente." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG":::

4. Para **URI de redirecionamento**, insira *https://localhost:44323* .  Selecione **Adicionar** e, em seguida, selecione **Avançar**.

5.  Na página **configurar credenciais do aplicativo** : 
    1. Selecione **gerar um segredo compartilhado**. 
    1. Copie o segredo. Você usará esse segredo posteriormente no arquivo de *web.config* do aplicativo. É o valor para `ida:ClientSecret` .  
    1. Selecione **Avançar**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG" alt-text="Captura de tela que mostra a página configurar credenciais do aplicativo." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG":::

6. Na página **Configurar API da Web** : 
    1. Para **identificador**, insira *https://contoso.com/WebApp* . Você usará esse valor posteriormente no arquivo de *web.config* do aplicativo. É o valor para `ida:GraphResourceId` . 
    1. Selecione **Adicionar**. 
    1. Selecione **Avançar**.  

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG" alt-text="Captura de tela que mostra a página Configurar a Web A P." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG":::

7. Na página **aplicar política de controle de acesso** , selecione **permitir todos**. Em seguida, selecione **Avançar**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG" alt-text="Captura de tela que mostra a página aplicar política de controle de acesso." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG":::

8. Na página **configurar permissões de aplicativo** , verifique se **OpenID** e **user_impersonation** estão selecionados. Em seguida, selecione **Avançar**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG" alt-text="Captura de tela que mostra a página configurar permissões de aplicativo." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG":::

9. Na página **Resumo** , selecione **Avançar**.

10. Na página **concluir** , selecione **fechar**.

## <a name="upgrade-the-database"></a>Atualizar o banco de dados
Este artigo se baseia no Visual Studio 2015. Para fazer com que o exemplo funcione com o Visual Studio 2015, atualize o arquivo de banco de dados seguindo as instruções nesta seção.

Esta seção discute como baixar a API Web de exemplo e atualizar o banco de dados no Visual Studio 2015. Usamos o [exemplo de Azure Active Directory](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity).

Para baixar o projeto de exemplo, em git bash, insira o seguinte comando:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git
```

![Captura de tela que mostra como baixar o projeto de exemplo.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)

Para atualizar o arquivo de banco de dados:

1.  Abra o projeto no Visual Studio. Na janela exibida, uma mensagem explica que o aplicativo requer o SQL Server 2012 Express. Se você não tiver SQL Server 2012 Express, precisará atualizar o banco de dados.  Selecione **OK**.

    ![Captura de tela que mostra uma mensagem explicando que o aplicativo requer o servidor Q L Server 2012 Express. Caso contrário, você precisa atualizar o banco de dados.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)

2. Na parte superior da janela, compile o aplicativo selecionando **Compilar** compilação  >  **solução**. Todos os pacotes NuGet serão restaurados.

    ![Captura de tela que mostra que a restauração dos pacotes NuGet foi bem-sucedida.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)

3.  Na parte superior da janela, selecione **Exibir**  >  **Gerenciador de servidores**.  No painel que é aberto, em **conexões de dados**, clique com o botão direito do mouse em **DefaultConnection** e selecione **Modify Connection**.

    ![Captura de tela que realça o item de menu Modificar conexão.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)

4.  Na janela **Modificar conexão** , em **nome do arquivo de banco de dados (novo ou existente)**, selecione **procurar**. Insira *path\filename.MDF*. Em seguida, na caixa de diálogo, selecione **Sim**.

    ![Captura de tela que mostra a caixa de diálogo para criar o arquivo de banco de dados.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)

5.  Na caixa de diálogo **Modificar conexão** , selecione **avançado**.

    ![Captura de tela que mostra o botão Avançado.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)

6.  Na caixa de diálogo **Propriedades avançadas** , em **fonte de dados**, altere **(LocalDb\v11.0)** para **(LocalDb) \MSSQLLocalDB**.

    ![Captura de tela que realça o campo da fonte de dados.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)

7.  Selecione **OK** > **OK**. Em seguida, selecione **Sim** para atualizar o banco de dados.

    ![Captura de tela que mostra a caixa de diálogo para atualizar o banco de dados.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)

8.  Depois que o processo for concluído, à direita, copie o valor no campo **cadeia de conexão** .

    ![Captura de tela que mostra o campo de cadeia de conexão.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)

9.  Abra o arquivo *web.config* e substitua o `connectionString` valor pelo valor que você copiou anteriormente.  Salve o arquivo de *web.config* .

    > [!NOTE]
    > As etapas anteriores são necessárias para que você possa obter a nova cadeia de conexão. Caso contrário, você receberá erros quando executar `Update-Database` posteriormente neste artigo.

    ![Captura de tela que mostra onde encontrar o valor da cadeia de conexão.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)

10. Na parte superior da janela do Visual Studio, selecione **Exibir**  >  **outro**  >  **console do Gerenciador de pacotes** do Windows.

    ![Captura de tela que realça o item de menu do console do Gerenciador de pacotes.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)

11. No painel de **console do Gerenciador de pacotes** , digite  `Enable-Migrations` .

    > [!NOTE]
    > Se você receber um erro dizendo "Enable-Migrations não é reconhecido como um cmdlet", insira *install-Package EntityFramework* para atualizar o Entity Framework.

    ![Captura de tela que mostra onde inserir enable-Migrations.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)

12. Insira `Add-Migration <AnyNameHere>`.

    ![Captura de tela que mostra onde inserir o teste de Add-Migration.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)

13. Insira `Update-Database`.

    ![Captura de tela que mostra onde inserir Update-Database.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)

## <a name="modify-the-web-api"></a>Modificar a API Web 

Para modificar a API Web de exemplo no Visual Studio:

1.  No Visual Studio, abra o exemplo.

2.  Abra o arquivo *web.config* .  Modifique as seguintes configurações usando os valores que você copiou no procedimento [criar um grupo de aplicativos](#create-an-application-group) :

    -   `ida:ClientId`: Insira a ID do cliente.

    -   `ida:ClientSecret`: Insira o segredo do cliente.

    -   `ida:GraphResourceId`: Insira a ID do recurso do grafo.

    ![Captura de tela que realça os valores que você deve alterar.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)

3. Em **App_Start**, abra o arquivo *Startup.auth.cs* . Faça as seguintes alterações:

    -   Comente as linhas a seguir:

        ```
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
        ```

    -   Em vez das linhas removidas, adicione a seguinte linha:

        ```
        public static readonly string Authority = "https://<your_fsname>/adfs";
        ```

        Aqui, substitua `<your_fsname>` pela parte DNS da URL do serviço de Federação. Por exemplo, digite *ADFS.contoso.com*.

        ![Captura de tela que mostra as alterações no arquivo C S de autenticação do ponto de inicialização.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)

4.  Abra o arquivo *UserProfileController.cs* . Faça as seguintes alterações:

    -   Comente a seguinte linha:

        ```
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));
        ```

    -   Substitua as duas ocorrências pelo código a seguir:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));
        ```

        ![Captura de tela que mostra as alterações no arquivo de ponto C S do controlador de perfil do usuário.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)

    -   Comente a seguinte linha:

        ```
        //authContext = new AuthenticationContext(Startup.Authority);
        ```

    -   Substitua as duas ocorrências pelo código a seguir:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false);
        ```

        ![Captura de tela que realça as alterações feitas no valor de authContext.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)

    -   Comente todas as instâncias da seguinte linha:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString() + "/OAuth");
        ```

    -   Substitua todas as ocorrências pelo seguinte código:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString());
        ```

        ![Captura de tela que realça o U R I redirecionar o valor U R I.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)

## <a name="test-the-solution"></a>Testar a solução

Para testar a solução de cliente confidencial:

1. Na parte superior da janela do Visual Studio, verifique se o **Internet Explorer** está selecionado. Em seguida, selecione a seta verde.

   ![Captura de tela que realça o botão do Internet Explorer.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)

2. Na página **ASP.net** que abre: 
    1. No canto superior direito, selecione **registrar**.  
    1. Insira um nome de usuário e uma senha. 
    1. Selecione **registrar** para criar uma conta local no banco de dados SQL.

   :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG" alt-text="Captura de tela que mostra onde criar uma conta local no banco de dados S Q L." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG":::

3. Observe a mensagem **Olá abby \@ contoso.com!**.  Selecione **perfil**.

   :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG" alt-text="Captura de tela que realça o perfil." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG":::

4. Na nova página, você verá uma mensagem solicitando que você entre.  Selecione **aqui**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG" alt-text="Captura de tela que mostra a página de perfil do usuário." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG":::

    Você será solicitado a entrar no AD FS.

   :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG" alt-text="Captura de tela que mostra a página de entrada para um D F S." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG":::     
        
## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre o [desenvolvimento de AD FS](../../ad-fs/AD-FS-Development.md).
