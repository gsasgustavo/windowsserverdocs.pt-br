---
description: 'Saiba mais sobre: criar um aplicativo do lado do servidor usando clientes confidenciais OAuth com o AD FS 2016 ou posterior'
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: Criar um aplicativo do lado do servidor usando clientes confidenciais OAuth com o AD FS 2016 ou posterior
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: fbf316e397d5d3423b046ed6a6b665555ab0cb18
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946392"
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016-or-later"></a>Criar um aplicativo do lado do servidor usando clientes confidenciais OAuth com o AD FS 2016 ou posterior


AD FS 2016 e versões posteriores fornecem suporte para clientes capazes de manter seu próprio segredo, como um aplicativo ou serviço em execução em um servidor Web.  Esses clientes são conhecidos como clientes confidenciais.
Abaixo está um esquema de um aplicativo Web em execução em um servidor Web e servindo como um cliente confidencial para AD FS:

## <a name="pre-requisites"></a>Pré-requisitos
Veja a seguir uma lista de pré-requisitos que são necessários antes de concluir este documento. Este documento pressupõe que AD FS foi instalado.

-   Ferramentas de cliente do GitHub

-   AD FS no Windows Server 2016 TP4 ou posterior

-   Visual Studio 2013 ou posterior.

## <a name="create-an-application-group-in-ad-fs-2016-or-later"></a>Criar um grupo de aplicativos no AD FS 2016 ou posterior
A seção a seguir descreve como configurar o grupo de aplicativos no AD FS 2016 ou posterior.

#### <a name="create-the-application-group"></a>Criar o grupo de aplicativos

1.  Em gerenciamento de AD FS, clique com o botão direito do mouse em grupos de aplicativos e selecione **Adicionar grupo de aplicativos**.

2.  No assistente de grupo de aplicativos, para o **nome** , insira **ADFSOAUTHCC** e, em **aplicativos cliente-servidor** , selecione o **aplicativo de servidor acessando um modelo de API Web** .  Clique em **Avançar**.

    ![Captura de tela que mostra onde selecionar o aplicativo de servidor acessando uma API da Web.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)

3.  Copie o valor do **identificador de cliente** .  Ele será usado posteriormente como o valor de **ida: ClientID** no arquivo de web.config de aplicativos.

    ![Captura de tela que mostra onde você pode copiar o valor do identificador de cliente de.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)

4.  Insira o seguinte para o **URI de redirecionamento:**  -  **https://localhost:44323** .  Clique em **Adicionar**. Clique em **Avançar**.

5.  Na tela **configurar credenciais do aplicativo** , faça um check-in **gerar um segredo compartilhado** e copie o segredo.  Isso será usado posteriormente como o valor de **ida: ClientSecret** no arquivo de web.config de aplicativos.  Clique em **Avançar**.

    ![Captura de tela que mostra as credenciais de configurar aplicativo.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)

6. Na tela **Configurar API da Web** , insira o seguinte para o **identificador**  -  **https://contoso.com/WebApp** .  Clique em **Adicionar**. Clique em **Avançar**.  Esse valor será usado posteriormente para **ida: GraphResourceId** no arquivo de web.config de aplicativos.

    ![Captura de tela que mostra as telas configurar API da Web.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)

7. Na tela **aplicar política de controle de acesso** , selecione **permitir todos** e clique em **Avançar**.

    ![Captura de tela que mostra as telas aplicar política de controle de acesso.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)

8. Na tela **configurar permissões de aplicativo** , verifique se **OpenID** e **user_impersonation** estão selecionados e clique em **Avançar**.

    ![Captura de tela que mostra as permissões para configurar o aplicativo.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)

9. Na tela **Resumo** , clique em **Avançar**.

10. Na tela **concluir** , clique em **fechar**.

## <a name="upgrade-the-database"></a>Atualizar o banco de dados
O Visual Studio 2015 foi usado para criar este passo a passos.   Para obter o exemplo que funciona com o Visual Studio 2015, você precisará atualizar o arquivo de banco de dados.  Use o procedimento a seguir para fazer isso.

Esta seção discute como baixar a API Web de exemplo e atualizar o banco de dados no Visual Studio 2015.   Usaremos o exemplo do Azure AD [aqui](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity).

Para baixar o projeto de exemplo, use git bash e digite o seguinte:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git
```

![Captura de tela que mostra como baixar o projeto de exemplo.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)

#### <a name="to-upgrade-the-database-file"></a>Para atualizar o arquivo de banco de dados

1.  Abra o projeto no Visual Studio. haverá um pop-up informando que o aplicativo requer o SQL Server 2012 Express ou será necessário atualizar o banco de dados.  Clique em OK.

    ![Captura de tela que mostra a mensagem informando que o aplicativo requer o SQL Server 2012 Express ou será necessário atualizar o banco de dados.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)

2.  Em seguida, compile o aplicativo selecionando Build-> Compilar solução na parte superior.  Isso irá restaurar todos os pacotes NuGet.

    ![Captura de tela que mostra que a restauração dos pacotes NuGet foi bem-sucedida.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)

3.  Agora, na parte superior, selecione **Exibir**  ->  **Gerenciador de servidores**.  Quando isso for aberto, em **conexões de dados**, clique com o botão direito do mouse em **DefaultConnection** e selecione **Modify Connection**.

    ![Captura de tela que realça a opção de menu Modificar conexão.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)

4.  Em **Modificar conexão**, em **nome do arquivo de banco de dados (novo ou existente)**, selecione **procurar** e forneça **path\filename.MDF**. Clique em **Sim** na caixa de diálogo.

    ![Captura de tela que mostra a caixa de diálogo para criar o arquivo de banco de dados.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)

5.  Em **Modificar conexão**, selecione **avançado**.

    ![Captura de tela que mostra o botão Avançado.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)

6.  Nas propriedades avançadas, localize a fonte de dados e use a lista suspensa para alterá-la de **(LocalDb\v11.0)** para **(LocalDb) \MSSQLLocalDB**.

    ![Captura de tela que realça o campo da fonte de dados.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)

7.  Clique em OK. Clique em OK.  Clique em Sim para atualizar o banco de dados.

    ![Captura de tela que mostra a caixa de diálogo para atualizar o banco de dados.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)

8.  Quando isso for concluído, à direita, copie o valor na caixa ao lado de cadeia de **conexão.**

    ![Captura de tela que mostra o campo de cadeia de conexão.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)

9.  Agora, abra o arquivo Web.config e substitua o valor que está em connectionString pelo valor que você copiou acima.  Salve o arquivo Web. config.

    > [!NOTE]
    > As etapas acima são necessárias para que possamos obter o novo connectionString.  Caso contrário, quando executarmos Update-Database abaixo, o erro será excedido.

    ![Captura de tela que mostra onde encontrar o valor da cadeia de conexão.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)

10. Na parte superior do Visual Studio, selecione **Exibir**  ->  **outro**  ->  **console do Gerenciador de pacotes** do Windows.

    ![Captura de tela que realça a opção de menu do console do Gerenciador de pacotes.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)

11. Na parte inferior, no console do Gerenciador de pacotes, digite:  `Enable-Migrations` e pressione Enter.

    > [!NOTE]
    > Se você receber um erro que diz Enable-Migrations não é reconhecido como um cmdlet, insira Install-Package EntityFramework para atualizar o EntityFramework.

    ![Sceenshot que mostra onde inserir enable-Migrations.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)

12. Na parte inferior, no console do Gerenciador de pacotes, digite:  `Add-Migration <anynamehere>` e pressione Enter.

    ![Captura de tela que mostra onde inserir Add-Migration teste.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)

13. Na parte inferior, no console do Gerenciador de pacotes, digite:  `Update-Database` e pressione Enter.

    ![Captura de tela que mostra onde inserir Update-Database.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)

## <a name="modify-the-webapi-in-visual-studio"></a>Modificar o WebApi no Visual Studio

#### <a name="to-modify-the-sample-web-api"></a>Para modificar a API Web de exemplo

1.  Abra o exemplo usando o Visual Studio.

2.  Abra o arquivo web.config.  Modifique os seguintes valores:

    -   Ida: ClientId – Insira o valor de #3 na seção criar o grupo de aplicativos acima.

    -   Ida: ClientSecret-Insira o valor de #5 na seção criar o grupo de aplicativos acima.

    -   Ida: GraphResourceId-Insira o valor de #6 na seção criar o grupo de aplicativos acima.

    ![Captura de tela que realça os valores que você deve alterar.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)

3.  Abra o arquivo Startup.Auth.cs em App_Start e faça as seguintes alterações:

    -   Comente as linhas a seguir:

        ```
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
        ```

    -   Adicione o seguinte em seu lugar:

        ```
        public static readonly string Authority = "https://<your_fsname>/adfs";
        ```

        em que <your_fsname> é substituído pela parte DNS da URL do serviço de Federação, por exemplo, adfs.contoso.com

        ![Captura de tela que mostra as alterações no arquivo C S de autenticação do ponto de inicialização.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)

4.  Abra o arquivo UserProfileController.cs e faça as seguintes alterações:

    -   Comente o seguinte:

        ```
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));
        ```

    -   Substitua as duas ocorrências pelo seguinte:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));
        ```

        ![Captura de tela que mostra as alterações no arquivo de ponto C S do controlador de perfil do usuário.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)

    -   Comente o seguinte:

        ```
        //authContext = new AuthenticationContext(Startup.Authority);
        ```

    -   Substitua as duas ocorrências pelo seguinte:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false);
        ```

        ![Captura de tela que realça as alterações feitas no valor de authContext.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)

    -   Agora comente todas as instâncias do seguinte:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString() + "/OAuth");
        ```

    -   Substitua todas as ocorrências com o seguinte:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString());
        ```

        ![Captura de tela que destaca o que você está redirecionando... você é o valor i.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)

## <a name="test-the-solution"></a>Testar a solução
Nesta seção, testaremos a solução de cliente confidencial.  Use o procedimento a seguir para testar a solução.

#### <a name="testing-the-confidential-client-solution"></a>Testando a solução de cliente confidencial

1. Na parte superior do Visual Studio, verifique se o Internet Explorer está selecionado e clique na seta verde.

   ![Captura de tela que realça o botão do Internet Explorer.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)

2. Depois que a página ASP.Net aparecer, clique em **registrar** na parte superior direita da página.  Insira um nome de usuário e uma senha e clique no botão **registrar** .  Isso cria uma conta local no banco de dados SQL.

   ![Captura de tela que mostra onde criar uma conta local no banco de dados S Q L.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)

3. Observe agora que o site ASP.NET diz Olá abby@contoso.com !.  Clique em **Perfil**.

   ![Captura de tela que realça o perfil.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)

4. Isso abre uma página sem nenhuma informação e diz que devemos clicar aqui para entrar.  Clique **aqui**.

   ![Captura de tela que mostra a página de perfil do usuário.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)

5. Agora, você será solicitado a entrar no AD FS.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)

## <a name="next-steps"></a>Próximas etapas
[Desenvolvimento do AD FS](../../ad-fs/AD-FS-Development.md)
