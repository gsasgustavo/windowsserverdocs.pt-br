---
title: AD FS API Web MSAL chamando a API da Web (em nome do cenário)
description: Saiba como criar uma API da Web chamando outra API da Web.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.openlocfilehash: d5289caaa272931f2e96d6fafb410e9861896dfc
ms.sourcegitcommit: fc2a7c69a74edcd79372054c4a9a24237510babd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2021
ms.locfileid: "98672968"
---
# <a name="scenario-web-api-calling-web-api-on-behalf-of-scenario"></a>Cenário: API Web chamando a API da Web (em nome do cenário)
> Aplica-se a: AD FS 2019 e posterior

Saiba como criar uma API da Web chamando outra API da Web em nome do usuário.

Antes de ler este artigo, você deve estar familiarizado com os [conceitos de AD FS](../ad-fs-openid-connect-oauth-concepts.md) e o [fluxo Behalf_Of](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#on-behalf-of-flow)

## <a name="overview"></a>Visão geral


- Um cliente (aplicativo Web)-não representado no diagrama abaixo – chama uma API Web protegida e fornece um token de portador JWT em seu cabeçalho http "Authorization".
- A API Web protegida valida o token e usa o método MSAL [AcquireTokenOnBehalfOf](/dotnet/api/microsoft.identitymodel.clients.activedirectory.authenticationcontext.acquiretokenasync#Microsoft_IdentityModel_Clients_ActiveDirectory_AuthenticationContext_AcquireTokenAsync_System_String_Microsoft_IdentityModel_Clients_ActiveDirectory_ClientCredential_Microsoft_IdentityModel_Clients_ActiveDirectory_UserAssertion_)   para solicitar (de AD FS) outro token para que ele possa, por sua vez, chamar uma segunda API da Web (chamada de API da Web downstream) em nome do usuário.
- A API Web protegida usa esse token para chamar uma API downstream. Ele também pode chamar AcquireTokenSilentlater para solicitar tokens para outras APIs de downstream (mas ainda em nome do mesmo usuário).O AcquireTokenSilent atualiza o token quando necessário.

     ![visão geral](media/adfs-msal-web-api-web-api/webapi1.png)

Para entender melhor como configurar em nome do cenário de autenticação no ADFS, vamos usar um exemplo disponível [aqui](https://github.com/microsoft/adfs-sample-msal-dotnet-webapi-to-webapi-onbehalfof) e explicando as etapas de configuração de código e de registro do aplicativo.

## <a name="pre-requisites"></a>Pré-requisitos

- Ferramentas de cliente do GitHub
- AD FS 2019 ou posterior configurados e em execução
- Visual Studio 2013 ou posterior.

## <a name="app-registration-in-ad-fs"></a>Registro de aplicativo no AD FS

Esta seção mostra como registrar o aplicativo nativo como um cliente público e APIs Web como partes confiáveis (RP) no AD FS

  1. Em gerenciamento de AD FS, clique com o botão direito do mouse em **grupos de aplicativos** e selecione **Adicionar grupo de aplicativos**.

  2. No assistente de grupo de aplicativos, para o **nome** , insira **WebApiToWebApi** e, em **aplicativos cliente-servidor** , selecione o **aplicativo nativo acessando um modelo de API Web** . Clique em **Avançar**.

      ![Captura de tela da página inicial do assistente para Adicionar grupo de aplicativos mostrando o aplicativo nativo que está acessando um modelo de API Web realçado.](media/adfs-msal-web-api-web-api/webapi2.png)

  3. Copie o valor do **identificador de cliente** . Ele será usado posteriormente como o valor de **ClientID** no arquivo de **App.config** do aplicativo. Insira o seguinte para o **URI de redirecionamento:**  -  https://ToDoListClient . Clique em **Adicionar**. Clique em **Avançar**.

      ![Captura de tela da página do aplicativo nativo do assistente para Adicionar grupo de aplicativos mostrando o s R I de redirecionamento.](media/adfs-msal-web-api-web-api/webapi3.png)

  4. Na tela configurar API da Web, insira o **identificador:** https://localhost:44321/ . Clique em **Adicionar**. Clique em **Avançar**. Esse valor será usado posteriormente nos arquivos de **App.config** e **Web.Config** do aplicativo.

      ![Captura de tela da página Configurar API da Web do assistente para Adicionar grupo de aplicativos mostrando o identificador correto.](media/adfs-msal-web-api-web-api/webapi4.png)

  5. Na tela aplicar política de controle de acesso, selecione **permitir todos** e clique em **Avançar**.

      ![Captura de tela da página escolher política de controle de acesso do assistente para Adicionar grupo de aplicativos mostrando a opção permitir todos realçada.](media/adfs-msal-web-api-web-api/webapi5.png)

  6. Na tela configurar permissões de aplicativo, selecione **OpenID** e **user_impersonation**. Clique em **Avançar**.

      ![Captura de tela da página configurar permissões de aplicativo do assistente para Adicionar grupo de aplicativos mostrando abrir I D selecionado.](media/adfs-msal-web-api-web-api/webapi6.png)

  7. Na tela Resumo, clique em **Avançar**.

  8. Na tela concluir, clique em **fechar**.


  9. Em gerenciamento de AD FS, clique em **grupos de aplicativos** e selecione grupo de aplicativos **WebApiToWebApi** . Clique com o botão direito do mouse e selecione **Propriedades**.

      ![Captura de tela da caixa de diálogo de gerenciamento a D S mostrando o grupo WebApiToWebApi realçado e a opção Propriedades na lista suspensa.](media/adfs-msal-web-api-web-api/webapi7.png)

  10. Na tela de propriedades do WebApiToWebApi, clique em **Adicionar aplicativo...**.

      ![Captura de tela da caixa de diálogo Propriedades do WebApiToWebApi mostrando o aplicativo WebApiToWebApi-Web a P listado.](media/adfs-msal-web-api-web-api/webapi8.png)

  11. Em aplicativos autônomos, selecione **aplicativo de servidor**.

      ![Captura de tela da página inicial do assistente Adicionar um novo aplicativo ao WebApiToWebApi mostrando a opção aplicativo do servidor realçada.](media/adfs-msal-web-api-web-api/webapi9.png)

  12. Na tela de aplicativo de servidor, adicione https://localhost:44321/ como o **identificador de cliente** e o **URI de redirecionamento**.

      ![Captura de tela da página de aplicativo do servidor do assistente Adicionar um novo aplicativo ao WebApiToWebApi mostrando o identificador de cliente correto e redirecionar U R I.](media/adfs-msal-web-api-web-api/webapi10.png)

  13. Na tela configurar credenciais do aplicativo, selecione **gerar um segredo compartilhado**. Copie o segredo para uso posterior.

      ![Captura de tela da página Configurar aplicativo de credenciais de aplicativo do assistente para adicionar um novo aplicativo ao WebApiToWebApi mostrando a opção gerar um segredo compartilhado selecionada e o segredo compartilhado gerado realçado.](media/adfs-msal-web-api-web-api/webapi11.png)

  14. Na tela Resumo, clique em **Avançar**.

  15. Na tela concluir, clique em **fechar**.

  16. Em gerenciamento de AD FS, clique em **grupos de aplicativos** e selecione grupo de aplicativos **WebApiToWebApi** . Clique com o botão direito do mouse e selecione **Propriedades**.

      ![Segunda captura de tela da caixa de diálogo de gerenciamento de D F S mostrando o grupo WebApiToWebApi realçado e a opção Propriedades na lista suspensa.](media/adfs-msal-web-api-web-api/webapi12.png)

  17. Na tela de propriedades do WebApiToWebApi, clique em **Adicionar aplicativo...**.

      ![Segunda captura de tela da caixa de diálogo Propriedades do WebApiToWebApi mostrando o aplicativo WebApiToWebApi-Web A P listado.](media/adfs-msal-web-api-web-api/webapi13.png)

  18. Em aplicativos autônomos, selecione **API Web**.

      ![Captura de tela da página inicial do assistente Adicionar um novo aplicativo ao WebApiToWebApi mostrando a opção P I realçada da Web a.](media/adfs-msal-web-api-web-api/webapi14.png)

  19. Em configurar API Web, adicione https://localhost:44300 como o **identificador**.

      ![Captura de tela da página Configurar na Web A P do assistente para adicionar um novo aplicativo ao WebApiToWebApi mostrando o U R I de redirecionamento correto.](media/adfs-msal-web-api-web-api/webapi15.png)

  20. Na tela aplicar política de controle de acesso, selecione **permitir todos** e clique em **Avançar**.

      ![Captura de tela da página escolher política de controle de acesso do assistente Adicionar um novo aplicativo ao WebApiToWebApi mostrando a opção permitir todos realçada.](media/adfs-msal-web-api-web-api/webapi16.png)

  21. Na tela configurar permissões de aplicativo, clique em **Avançar**.

      ![Captura de tela da página configurar permissões de aplicativo do assistente para adicionar um novo aplicativo ao WebApiToWebApi mostrando a próxima opção chamada out.](media/adfs-msal-web-api-web-api/webapi17.png)

  22. Na tela Resumo, clique em **Avançar**.

  23. Na tela concluir, clique em **fechar**.

  24. Clique em OK em WebApiToWebApi – tela de propriedades da API Web 2

  25. Na tela de propriedades do WebApiToWebApi, selecione **WebApiToWebApi – API Web** e clique em **Editar...**.

      ![Captura de tela da caixa de diálogo Propriedades do WebApiToWebApi mostrando o aplicativo WebApiToWebApi-Web a P realçado.](media/adfs-msal-web-api-web-api/webapi18.png)

  26. Na tela WebApiToWebApi – Propriedades da API Web, selecione a guia **regras de transformação de emissão** e clique em **Adicionar regra..**..

      ![Captura de tela da caixa de diálogo Propriedades do P-Web WebApiToWebApi que mostra a guia regras de transformação de emissão.](media/adfs-msal-web-api-web-api/webapi19.png)

  27. Em Adicionar Assistente de regra de declaração de transformação, selecione **enviar declarações usando uma regra personalizada** do menu suspenso e clique em **Avançar**.

      ![Captura de tela da página Selecionar modelo de regra do assistente para Adicionar regra de declaração de transformação mostrando a opção enviar declarações usando uma regra personalizada selecionada.](media/adfs-msal-web-api-web-api/webapi20.png)

  28. Insira **PassAllClaims** no **nome da regra de declaração:** campo e **x: [] => problema (declaração = x);** regra de declaração no campo regra personalizada: e clique em concluir.

      ![Captura de tela da página Configurar regra do assistente para Adicionar regra de declaração de transformação mostrando a configuração explicada acima.](media/adfs-msal-web-api-web-api/webapi21.png)

  29. Clique em OK em WebApiToWebApi – tela de propriedades da API Web

  30. Na tela de propriedades do WebApiToWebApi, selecione Selecionar WebApiToWebApi – API Web 2 e clique em Editar...</br>
  ![Captura de tela da caixa de diálogo Propriedades do WebApiToWebApi mostrando o WebApiToWebApi do aplicativo P I 2 da Web a ser realçado.](media/adfs-msal-web-api-web-api/webapi22.png)

  31. Na tela WebApiToWebApi – Propriedades da API Web 2, selecione a guia regras de transformação de emissão e clique em Adicionar regra...

  32. Em Adicionar Assistente de regra de declaração de transformação, selecione enviar declarações usando uma regra personalizada do menu suspenso e clique ![ na próxima captura de tela da página Selecionar modelo de regra do assistente para Adicionar regra de declaração de transformação, mostrando a opção enviar declarações usando uma regra personalizada selecionada.](media/adfs-msal-web-api-web-api/webapi23.png)

  33. Insira PassAllClaims no nome da regra de declaração: campo e **x: [] => problema (declaração = x);** regra de declaração no campo **regra personalizada:** e clique em **concluir**.

      ![Segunda captura de tela da página Configurar regra do assistente Adicionar regra de declaração de transformação mostrando a configuração explicada acima.](media/adfs-msal-web-api-web-api/webapi24.png)

  34.  Clique em OK na tela WebApiToWebApi – Propriedades da API Web 2 e, em seguida, na tela Propriedades de WebApiToWebApi.


## <a name="code-configuration"></a>Configuração de código

Esta seção mostra como configurar uma API Web para chamar outra API da Web

  1. Baixe o [exemplo daqui](https://github.com/microsoft/adfs-sample-msal-dotnet-webapi-to-webapi-onbehalfof)

  2. Abrir o exemplo usando o Visual Studio

  3. Abra o arquivo App.config. Modifique o seguinte:
       - Ida: Authority-insira https://[seu nome de host do AD FS]/ADFS/
       - Ida: ClientId – Insira o valor de #3 no registro do aplicativo na seção AD FS acima.
       - Ida: RedirectUri-Insira o valor de #3 no registro do aplicativo na seção AD FS acima.
       - todo: TodoListResourceId – Insira o valor do identificador de #4 no registro do aplicativo na seção AD FS acima
       - Ida: todo: TodoListBaseAddress-Insira o valor do identificador de #4 no registro do aplicativo na seção AD FS acima.

            ![Captura de tela do arquivo de configuração do aplicativo mostrando os valores modificados.](media/adfs-msal-web-api-web-api/webapi25.png)

  4. Abra o arquivo Web.config em ToDoListService. Modifique o seguinte:
       - Ida: Audience-Insira o valor do identificador de cliente de #12 no registro do aplicativo na seção AD FS acima
       - Ida: ClientId – Insira o valor do identificador de cliente de #12 no registro do aplicativo na seção AD FS acima.
       - Ida: ClientSecret-Insira o segredo compartilhado copiado de #13 no registro do aplicativo na seção AD FS acima.
       - Ida: RedirectUri-Insira o valor de RedirectUri de #12 no registro do aplicativo na seção AD FS acima.
       - Ida: AdfsMetadataEndpoint-insira https://[seu nome de host do AD FS]/FederationMetadata/2007-06/federationmetadata.xml
       - Ida: OBOWebAPIBase-Insira o valor do identificador de #19 no registro do aplicativo na seção AD FS acima.
       - Ida: Authority-insira https://[seu nome de host do AD FS]/ADFS

          ![Captura de tela do arquivo de configuração da Web em ToDoListService mostrando os valores modificados.](media/adfs-msal-web-api-web-api/webapi26.png)

 5. Abra o arquivo Web.config em WebAPIOBO. Modifique o seguinte:
       - Ida: AdfsMetadataEndpoint-insira https://[seu nome de host do AD FS]/FederationMetadata/2007-06/federationmetadata.xml
       - Ida: Audience-Insira o valor do identificador de cliente de #12 no registro do aplicativo na seção AD FS acima

          ![Captura de tela do arquivo de configuração da Web em WebAPIOBO mostrando os valores modificados.](media/adfs-msal-web-api-web-api/webapi27.png)

## <a name="test-the-sample"></a>O exemplo de teste

Esta seção mostra como testar o exemplo configurado acima.

Depois que as alterações de código forem feitas para recompilar a solução

  1. No Visual Studio, clique com o botão direito do mouse em solução e selecione **definir projetos de inicialização...**

      ![Captura de tela da lista que aparece quando você clica com o botão direito do mouse na solução com a opção definir projetos de inicialização realçada.](media/adfs-msal-web-api-web-api/webapi28.png)

  2. Nas páginas de propriedades, verifique se a **ação** está definida como **Iniciar** para cada um dos projetos, exceto TodoListSPA.

      ![Captura de tela da caixa de diálogo páginas de propriedades da solução mostrando a opção vários projetos de inicialização selecionada e todas as ações do projeto definidas como iniciar.](media/adfs-msal-web-api-web-api/webapi29.png)

  3. Na parte superior do Visual Studio, clique na seta verde.

      ![Captura de tela da interface do usuário do Visual Studio com a opção de início chamada out.](media/adfs-msal-web-api-web-api/webapi30.png)

  4. Na tela principal do aplicativo nativo, clique em **entrar**.

      ![Captura de tela da caixa de diálogo do cliente lista de tarefas.](media/adfs-msal-web-api-web-api/webapi31.png)

     Se você não vir a tela do aplicativo nativo, pesquise e remova os arquivos * msalcache. bin da pasta em que o repositório do projeto é salvo em seu sistema.

  5. Você será direcionado novamente para a página de entrada AD FS. Vá em frente e entre.

      ![Captura de tela da página de entrada.](media/adfs-msal-web-api-web-api/webapi32.png)

  6. Depois de conectado, insira texto API da Web para chamada à API Web no **criar um item de tarefas pendentes**. Clique em **Adicionar item**.  Isso chamará a API da Web (serviço de lista de tarefas) que, em seguida, chama a API da Web 2 (WebAPIOBO) e adiciona o item no cache.

      ![Captura de tela da caixa de diálogo do cliente lista de tarefas com o novo item a ser feito preenchendo a seção tarefas pendentes.](media/adfs-msal-web-api-web-api/webapi33.png)

 ## <a name="next-steps"></a>Próximas etapas
[Fluxos e cenários de aplicativo do AD FS OpenID Connect/OAuth](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)


