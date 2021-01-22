---
title: AD FS a API Web de chamada de aplicativo nativo do MSAL
description: Ganhe instruções para criar um aplicativo nativo autenticado por usuários AD FS 2019 e adquirir tokens usando a biblioteca MSAL para chamar APIs da Web.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.openlocfilehash: 88333427cf8f147e0d81d8d07dfff08fb2cebb09
ms.sourcegitcommit: fc2a7c69a74edcd79372054c4a9a24237510babd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2021
ms.locfileid: "98672958"
---
# <a name="scenario-native-app-calling-web-api"></a>Cenário: API Web de chamada de aplicativo nativo
>Aplica-se a: AD FS 2019 e posterior

Saiba como criar um aplicativo nativo autenticando usuários com autenticação AD FS 2019 e adquirindo tokens usando a [biblioteca MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki)  para chamar APIs da Web.

Antes de ler este artigo, você deve estar familiarizado com os [conceitos de AD FS](../ad-fs-openid-connect-oauth-concepts.md) e o fluxo de concessão de código de [autorização](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#authorization-code-grant-flow)

## <a name="overview"></a>Visão geral

 ![Visão geral](media/adfs-msal-native-app-web-api/native1.png)

Nesse fluxo, você adiciona autenticação ao seu aplicativo nativo (cliente público), que, portanto, pode conectar usuários e chamar uma API da Web. Para chamar uma API Web de um aplicativo nativo que assina usuários, você pode usar o método de aquisição de token [AcquireTokenInteractive](/dotnet/api/microsoft.identity.client.ipublicclientapplication.acquiretokeninteractive#Microsoft_Identity_Client_IPublicClientApplication_AcquireTokenInteractive_System_Collections_Generic_IEnumerable_System_String__) do MSAL. Para permitir essa interação, a MSAL aproveita um navegador da Web.

Para entender melhor como configurar um aplicativo nativo no ADFS para adquirir o token de acesso interativamente, vamos usar um exemplo disponível [aqui](https://github.com/microsoft/adfs-sample-msal-dotnet-native-to-webapi) e explicando as etapas de configuração de código e de registro do aplicativo.


## <a name="pre-requisites"></a>Pré-requisitos

- Ferramentas de cliente do GitHub
- AD FS 2019 ou posterior configurados e em execução
- Visual Studio 2013 ou posterior.

## <a name="app-registration-in-ad-fs"></a>Registro de aplicativo no AD FS
Esta seção mostra como registrar o aplicativo nativo como um cliente público e uma API Web como uma terceira parte confiável (RP) no AD FS

  1. Em **Gerenciamento de AD FS**, clique com o botão direito do mouse em **grupos de aplicativos** e selecione **Adicionar grupo de aplicativos**.

  2. No assistente de grupo de aplicativos, para o **nome** , insira **NativeAppToWebApi** e, em **aplicativos cliente-servidor** , selecione o **aplicativo nativo acessando um modelo de API Web** . Clique em **Avançar**.

      ![Captura de tela da página inicial do assistente para Adicionar grupo de aplicativos mostrando o aplicativo nativo que está acessando um modelo de API Web realçado.](media/adfs-msal-native-app-web-api/native2.png)

  3. Copie o valor do **identificador de cliente** . Ele será usado posteriormente como o valor de **ClientID** no arquivo de **App.config** do aplicativo. Insira o seguinte para o **URI de redirecionamento:** https://ToDoListClient . Clique em **Adicionar**. Clique em **Avançar**.

     ![Captura de tela da página do aplicativo nativo do assistente para Adicionar grupo de aplicativos mostrando o s R I de redirecionamento.](media/adfs-msal-native-app-web-api/native3.png)

  4. Na tela configurar API da Web, insira o **identificador:** https://localhost:44321/ . Clique em **Adicionar**. Clique em **Avançar**. Esse valor será usado posteriormente nos arquivos de **App.config** e **Web.config** do aplicativo.

     ![Captura de tela da página Configurar API da Web do assistente para Adicionar grupo de aplicativos mostrando o identificador correto.](media/adfs-msal-native-app-web-api/native4.png)

  5. Na tela aplicar política de controle de acesso, selecione **permitir todos** e clique em **Avançar**.

     ![Captura de tela da página escolher política de controle de acesso do assistente para Adicionar grupo de aplicativos mostrando a opção permitir todos realçada.](media/adfs-msal-native-app-web-api/native5.png)

  6. Na tela configurar permissões de aplicativo, verifique se **OpenID** está selecionado e clique em **Avançar**.

     ![Captura de tela da página configurar permissões de aplicativo do assistente para Adicionar grupo de aplicativos mostrando abrir I D selecionado.](media/adfs-msal-native-app-web-api/native6.png)

  7. Na tela Resumo, clique em **Avançar**.

  8. Na tela concluir, clique em **fechar**.

  9. Em gerenciamento de AD FS, clique em **grupos de aplicativos** e selecione grupo de aplicativos **NativeAppToWebApi**         . Clique com o botão direito do mouse e selecione **Propriedades**.

      ![Captura de tela da caixa de diálogo de gerenciamento a D S mostrando o grupo NativeAppToWebApi realçado e a opção Propriedades na lista suspensa.](media/adfs-msal-native-app-web-api/native7.png)

  10. Na tela de propriedades do NativeAppToWebApi, selecione **NativeAppToWebApi – API Web** em **API da Web** e clique em **Editar..** .

      ![Captura de tela da caixa de diálogo Propriedades do NativeAppToWebApi mostrando o aplicativo NativeAppToWebApi-Web a P realçado.](media/adfs-msal-native-app-web-api/native8.png)

  11. Na tela NativeAppToWebApi – Propriedades da API Web, selecione a guia **regras de transformação de emissão** e clique em **Adicionar regra..** .

      ![Captura de tela da caixa de diálogo Propriedades do P-Web NativeAppToWebApi que mostra a guia regras de transformação de emissão.](media/adfs-msal-native-app-web-api/native9.png)

  12. Em Adicionar Assistente de regra de declaração de transformação, selecione **transformar uma declaração de entrada** do **modelo de regra de declaração:** menu suspenso e clique em **Avançar**.

      ![Captura de tela da página Selecionar modelo de regra do assistente para Adicionar regra de declaração de transformação mostrando a opção transformar uma declaração de entrada selecionada.](media/adfs-msal-native-app-web-api/native10.png)

  13. Insira **NameID** no campo **nome da regra de declaração:** . Selecione o **nome** para o **tipo de declaração de entrada:**, **ID de nome** para tipo de **declaração de saída:** e **nome comum** para **formato de ID de nome de saída:**. clique em **concluir**.

      ![Captura de tela da página Configurar regra do assistente para Adicionar regra de declaração de transformação mostrando a configuração explicada acima.](media/adfs-msal-native-app-web-api/native11.png)

  14. Clique em OK em NativeAppToWebApi – tela de propriedades da API Web e, em seguida, NativeAppToWebApi tela de propriedades.

## <a name="code-configuration"></a>Configuração de código
Esta seção mostra como configurar um aplicativo nativo para o usuário de entrada e recuperar o token para chamar a API da Web

1. Baixe o [exemplo daqui](https://github.com/microsoft/adfs-sample-msal-dotnet-native-to-webapi)

2. Abrir o exemplo usando o Visual Studio

3. Abra o arquivo App.config. Modifique o seguinte:
   - Ida: Authority-Enter h`ttps://[your AD FS hostname]/adfs`
   - Ida: ClientId – Insira o valor do **identificador de cliente** de #3 no registro do aplicativo na seção AD FS acima.
   - Ida: RedirectUri-Insira o valor do **URI de redirecionamento** de #3 no registro do aplicativo na seção AD FS acima.
   - todo: TodoListResourceId – Insira o valor do **identificador** de #4 no registro do aplicativo na seção AD FS acima
   - Ida: todo: TodoListBaseAddress-Insira o valor do **identificador** de #4 no registro do aplicativo na seção AD FS acima.

     ![Captura de tela do arquivo de configuração do aplicativo mostrando os valores modificados.](media/adfs-msal-native-app-web-api/native12.png)

 4. Abra o arquivo Web.config. Modifique o seguinte:
    - Ida: Audience-Insira o valor do **identificador** de #4 no registro do aplicativo na seção AD FS acima
    - Ida: AdfsMetadataEndpoint-Enter `https://[your AD FS hostname]/federationmetadata/2007-06/federationmetadata.xml`

      ![Captura de tela do arquivo de configuração da Web mostrando os valores modificados.](media/adfs-msal-native-app-web-api/native13.png)

## <a name="test-the-sample"></a>O exemplo de teste
Esta seção mostra como testar o exemplo configurado acima.

  1. Depois que as alterações de código forem feitas para recompilar a solução

  2. No Visual Studio, clique com o botão direito do mouse em solução e selecione **definir projetos de inicialização...**

     ![Captura de tela da lista que aparece quando você clica com o botão direito do mouse na solução com a opção definir projetos de inicialização realçada.](media/adfs-msal-native-app-web-api/native14.png)

  3. Nas páginas de propriedades, verifique se a **ação** está definida como **Iniciar** para cada um dos projetos

     ![Captura de tela da caixa de diálogo páginas de propriedades da solução mostrando a opção vários projetos de inicialização selecionada e todas as ações do projeto definidas como iniciar.](media/adfs-msal-native-app-web-api/native15.png)

  4. Na parte superior do Visual Studio, clique na seta verde.

     ![Captura de tela da interface do usuário do Visual Studio com a opção de início chamada out.](media/adfs-msal-native-app-web-api/native16.png)

  5. Na tela principal do aplicativo nativo, clique em **entrar**.

     ![Captura de tela da caixa de diálogo do cliente lista de tarefas.](media/adfs-msal-native-app-web-api/native17.png)

   Se você não vir a tela do aplicativo nativo, pesquise e remova os `*msalcache.bin` arquivos da pasta em que o repositório do projeto é salvo em seu sistema.

  1. Você será direcionado novamente para a página de entrada AD FS. Vá em frente e entre.

      ![Captura de tela da página de entrada.](media/adfs-msal-native-app-web-api/native18.png)

  2. Depois de conectado, insira texto **Compilar aplicativo nativo para API Web** no **criar um item de tarefas pendentes**. Clique em **Adicionar item**.  Isso chamará o **serviço de lista de tarefas pendentes (API Web)** e adicionará o item no cache.

       ![Captura de tela da caixa de diálogo do cliente lista de tarefas com o novo item a ser feito preenchendo a seção tarefas pendentes.](media/adfs-msal-native-app-web-api/native19.png)

## <a name="next-steps"></a>Próximas etapas
[Fluxos e cenários de aplicativo do AD FS OpenID Connect/OAuth](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
