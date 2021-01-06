---
description: 'Saiba mais sobre: criar um aplicativo Web usando o OpenID Connect com o AD FS 2016 e posterior'
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: Criar um aplicativo Web usando o OpenID Connect com o AD FS 2016 e posterior
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: f0156ef18ba56aade897b86669f428db7239e63b
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946182"
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016-and-later"></a>Criar um aplicativo Web usando o OpenID Connect com o AD FS 2016 e posterior

## <a name="pre-requisites"></a>Pré-requisitos
Veja a seguir uma lista de pré-requisitos que são necessários antes de concluir este documento. Este documento pressupõe que AD FS foi instalado e um farm de AD FS foi criado.

-   Ferramentas de cliente do GitHub

-   AD FS no Windows Server 2016 TP4 ou posterior

-   Visual Studio 2013 ou posterior.

## <a name="create-an-application-group-in-ad-fs-2016-and-later"></a>Criar um grupo de aplicativos no AD FS 2016 e posterior
A seção a seguir descreve como configurar o grupo de aplicativos no AD FS 2016 e posterior.

#### <a name="create-application-group"></a>Criar grupo de aplicativos

1.  Em gerenciamento de AD FS, clique com o botão direito do mouse em grupos de aplicativos e selecione **Adicionar grupo de aplicativos**.

2.  No assistente de grupo de aplicativos, para o nome, insira **ADFSSSO** e, em **aplicativos cliente-servidor** , selecione o **navegador da Web acessando um modelo de aplicativo Web** .  Clique em **Avançar**.

    ![Captura de tela que realça o navegador da Web acessando um modelo de aplicativo Web.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)

3.  Copie o valor do **identificador de cliente** .  Ele será usado posteriormente como o valor de ida: ClientId no arquivo de web.config de aplicativos.

4.  Insira o seguinte para o **URI de redirecionamento:**  -  **https://localhost:44320/** .  Clique em **Adicionar**. Clique em **Avançar**.

    ![Captura de tela que mostra onde inserir o valor do U R I de redirecionamento.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)

5.  Na tela **Resumo** , clique em **Avançar**.

    ![Captura de tela que mostra o resumo.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)

6.  Na tela **concluir** , clique em **fechar**.

## <a name="download-and-modify-sample-application-to-authenticate-via-openid-connect-and-ad-fs"></a>Baixar e modificar o aplicativo de exemplo para autenticar via OpenID Connect e AD FS
Esta seção discute como baixar o aplicativo Web de exemplo e modificá-lo no Visual Studio.   Usaremos o exemplo do Azure AD [aqui](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect).

Para baixar o projeto de exemplo, use git bash e digite o seguinte:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect
```

![Captura de tela de uma janela de terminal que mostra como baixar o projeto de exemplo.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)

#### <a name="to-modify-the-app"></a>Para modificar o aplicativo

1.  Abra o exemplo usando o Visual Studio.

2.  Recompile o aplicativo para que todos os NuGets ausentes sejam restaurados.

3.  Abra o arquivo web.config.  Modifique os valores a seguir para que a aparência seja parecida com a seguinte:

    ```
    <add key="ida:ClientId" value="[Replace this Client Id from #3 in above section]" />
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with Redirect URI from #4 in the above section]" />
    ```

    ![Captura de tela que realça as alterações feitas no arquivo de configuração de ponto da Web.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)

4.  Abra o arquivo Startup.Auth.cs e faça as seguintes alterações:

    -   Comente o seguinte:

        ```
        //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
        ```

    -   Ajuste a lógica de inicialização do middleware OpenId Connect com as seguintes alterações:

        ```
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];
        ```

        ![Captura de tela que mostra como alterar a lógica de inicialização do middleware de conexão aberta I.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)

    -   Além disso, modifique as opções de middleware do OpenId Connect, como no seguinte:

        ```
        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                ClientId = clientId,
                //Authority = authority,
                MetadataAddress = metadataAddress,
                PostLogoutRedirectUri = postLogoutRedirectUri,
                RedirectUri = postLogoutRedirectUri
        ```

        ![Captura de tela que mostra como modificar as opções de middleware Open I D Connect.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)

        Alterando as opções acima, estamos fazendo o seguinte:

        -   Em vez de usar a autoridade para a comunicação de dados sobre o emissor confiável, especificamos o local do documento de descoberta diretamente por meio de MetadataAddress

        -   O Azure AD não impõe a presença de um redirect_uri na solicitação, mas o ADFS faz. Então, precisamos adicioná-lo aqui

## <a name="verify-the-app-is-working"></a>Verifique se o aplicativo está funcionando
Depois que as alterações acima tiverem sido feitas, pressione F5.  Isso abrirá a página de exemplo.  Clique em entrar.

![Captura de tela que mostra a página de exemplo a S P N E T.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)

Você será direcionado novamente para a página de entrada AD FS.  Vá em frente e entre.

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)

Quando isso for bem-sucedido, você verá que agora está conectado.

![Captura de tela que realça o nome de usuário que você usou para fazer logon.](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)

## <a name="next-steps"></a>Próximas etapas
[Desenvolvimento do AD FS](../../ad-fs/AD-FS-Development.md)
