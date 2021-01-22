---
title: AD FS aplicativo Web MSAL (aplicativo de servidor) chamando APIs da Web
description: Saiba como criar um aplicativo Web que assina usuários autenticados pelo AD FS 2019.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.openlocfilehash: e4f02400155dcb5899417b12e4c376fa3ee69fd0
ms.sourcegitcommit: fc2a7c69a74edcd79372054c4a9a24237510babd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2021
ms.locfileid: "98672948"
---
# <a name="scenario-web-app-server-app-calling-web-api"></a>Cenário: aplicativo Web (aplicativo de servidor) chamando API Web
>Aplica-se a: AD FS 2019 e posterior

Saiba como criar um aplicativo Web que assina usuários autenticados pelo AD FS 2019 e adquirindo tokens usando a [biblioteca MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki) para chamar APIs da Web.

Antes de ler este artigo, você deve estar familiarizado com os [conceitos de AD FS](../ad-fs-openid-connect-oauth-concepts.md) e o fluxo de concessão de código de [autorização](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#authorization-code-grant-flow)

## <a name="overview"></a>Visão geral

![Visão geral da API Web de chamada de aplicativo Web](media/adfs-msal-web-app-web-api/webapp1.png)

Nesse fluxo, você adiciona autenticação ao seu aplicativo Web (aplicativo de servidor), que, portanto, pode conectar usuários e chamar uma API da Web. No aplicativo Web, para chamar a API Web, use o método de aquisição de token [AcquireTokenByAuthorizationCode](/dotnet/api/microsoft.identity.client.acquiretokenbyauthorizationcodeparameterbuilder) da MSAL. Você usará o fluxo de código de autorização, armazenando o token adquirido no cache de token. Em seguida, o controlador adquirirá tokens silenciosamente do cache sempre que necessário. A MSAL atualiza o token, se necessário.

Aplicativos Web que chamam APIs da Web:


- são aplicativos cliente confidenciais.
- é por isso que eles registraram um segredo (segredo compartilhado do aplicativo, certificado ou conta do AD) com AD FS. Esse segredo é passado durante a chamada para AD FS para obter um token.

Para entender melhor como registrar um aplicativo Web no ADFS e configurá-lo para adquirir tokens para chamar uma API Web, vamos usar um exemplo disponível [aqui](https://github.com/microsoft/adfs-sample-msal-dotnet-webapp-to-webapi) e, em seguida, as etapas de registro do aplicativo e de configuração de código.


## <a name="pre-requisites"></a>Pré-requisitos

- Ferramentas de cliente do GitHub
- AD FS 2019 ou posterior configurados e em execução
- Visual Studio 2013 ou posterior.

## <a name="app-registration-in-ad-fs"></a>Registro de aplicativo no AD FS
Esta seção mostra como registrar o aplicativo Web como um cliente confidencial e uma API Web como uma terceira parte confiável (RP) no AD FS.

  1. Em gerenciamento de AD FS, clique com o botão direito do mouse em **grupos de aplicativos** e selecione **Adicionar grupo de aplicativos**.
  2. No assistente de grupo de aplicativos, para o **nome** , insira **WebAppToWebApi** e, em **aplicativos cliente-servidor** , selecione o **aplicativo de servidor acessando um modelo de API Web** . Clique em **Avançar**.

      ![Captura de tela da página inicial do assistente para Adicionar grupo de aplicativos mostrando o aplicativo de servidor que acessa um modelo P I realçado.](media/adfs-msal-web-app-web-api/webapp2.png)

  3. Copie o valor do **identificador de cliente** . Ele será usado posteriormente como o valor de **ida: ClientID** no arquivo de **Web.config** de aplicativos. Insira o seguinte para o **URI de redirecionamento:**  -  https://localhost:44326 . Clique em Adicionar. Clique em **Avançar**.

      ![Captura de tela da página de aplicativo do servidor do assistente para Adicionar grupo de aplicativos mostrando o identificador de cliente correto e redirecionar U R I.](media/adfs-msal-web-app-web-api/webapp3.png)

  4. Na tela configurar credenciais do aplicativo, faça um check-in **gerar um segredo compartilhado** e copie o segredo. Isso será usado posteriormente como o valor de **ida: ClientSecret** no arquivo de **Web.config** de aplicativos. Clique em **Avançar**.

      ![Captura de tela da página Configurar aplicativo de credenciais de aplicativo do assistente para Adicionar grupo de aplicativos mostrando a opção gerar um segredo compartilhado selecionada e o segredo compartilhado gerado preenchido.](media/adfs-msal-web-app-web-api/webapp4.png)

  5. Na tela configurar API da Web, insira o **identificador:** https://webapi . Clique em **Adicionar**. Clique em **Avançar**. Esse valor será usado posteriormente para **ida: GraphResourceId** no arquivo de **Web.config** de aplicativos.

      ![Captura de tela da página Configurar API da Web do assistente para Adicionar grupo de aplicativos mostrando o identificador correto.](media/adfs-msal-web-app-web-api/webapp5.png)

  6. Na tela aplicar política de controle de acesso, selecione **permitir** todos e clique em **Avançar**.

      ![Captura de tela da página escolher política de controle de acesso do assistente para Adicionar grupo de aplicativos mostrando a opção permitir todos realçada.](media/adfs-msal-web-app-web-api/webapp6.png)

  7. Na tela configurar permissões de aplicativo, verifique se **OpenID** e **user_impersonation** estão selecionados e clique em **Avançar**.

      ![Captura de tela da página configurar permissões de aplicativo do assistente para Adicionar grupo de aplicativos mostrando as opções abrir I D e representação do usuário selecionadas.](media/adfs-msal-web-app-web-api/webapp7.png)

  8. Na tela Resumo, clique em **Avançar**.

  9. Na tela concluir, clique em **fechar**.



## <a name="code-configuration"></a>Configuração de código

Esta seção mostra como configurar um aplicativo Web ASP.NET para o usuário de entrada e recuperar o token para chamar a API da Web

  1. Baixe o [exemplo daqui](https://github.com/microsoft/adfs-sample-msal-dotnet-webapp-to-webapi)

  2. Abrir o exemplo usando o Visual Studio

  3. Abra o arquivo web.config. Modifique o seguinte:
       - Ida: ClientId – Insira o valor do **identificador de cliente** de #3 no registro do aplicativo na seção AD FS acima.
       - Ida: ClientSecret-Insira o valor **secreto** de #4 no registro do aplicativo na seção AD FS acima.
       - Ida: RedirectUri-Insira o valor do **URI de redirecionamento** de #3 no registro do aplicativo na seção AD FS acima.
       - Ida: Authority-insira https://[seu nome de host do AD FS]/ADFS. Por exemplo, https://adfs.contoso.com/adfs
       - Ida: Resource – Insira o valor do **identificador** de #5 no registro do aplicativo na seção AD FS acima.

          ![Captura de tela do arquivo de configuração da Web mostrando os valores modificados.](media/adfs-msal-web-app-web-api/webapp8.png)


### <a name="test-the-sample"></a>O exemplo de teste
Esta seção mostra como testar o exemplo configurado acima.

  1. Depois que as alterações de código forem feitas para recompilar a solução

  2. Na parte superior do Visual Studio, verifique se o Internet Explorer está selecionado e clique na seta verde.

      ![Captura de tela da interface do usuário do Visual Studio com a opção IIS Express (Internet Explorer) chamada out.](media/adfs-msal-web-app-web-api/webapp9.png)

  3. Na Home Page, clique em entrar.

      ![Captura de tela da Home Page com a opção de entrada chamada out.](media/adfs-msal-web-app-web-api/webapp10.png)

  4. Você será direcionado novamente para a página de entrada AD FS. Vá em frente e entre.

      ![Captura de tela da página de entrada.](media/adfs-msal-web-app-web-api/webapp11.png)

  5. Depois de conectado, clique em token de acesso.

      ![Captura de tela da Home Page com a opção de token de acesso chamada out.](media/adfs-msal-web-app-web-api/webapp12.png)

  6. Clicar no token de acesso obterá as informações de token de acesso chamando a API da Web

      ![Captura de tela da página token de acesso mostrando as informações do token de acesso.](media/adfs-msal-web-app-web-api/webapp13.png)

 ## <a name="next-steps"></a>Próximas etapas
[Fluxos e cenários de aplicativo do AD FS OpenID Connect/OAuth](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)

