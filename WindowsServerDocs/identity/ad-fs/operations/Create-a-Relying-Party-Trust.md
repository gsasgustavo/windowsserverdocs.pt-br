---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: Criar um objeto de confiança de terceira parte confiável
description: Saiba como criar uma relação de confiança de terceira parte confiável manualmente e usar metadados de Federação.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 949ff74ea3fbb4518b1463709d798c945d1a3b5b
ms.sourcegitcommit: 6717decb5839aa340c81811d6fde020aabaddb3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98781907"
---
# <a name="create-a-relying-party-trust"></a>Criar um objeto de confiança de terceira parte confiável


O documento a seguir fornece informações sobre como criar uma relação de confiança de terceira parte confiável manualmente e usando metadados de Federação.

## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>Para criar um confiança de terceira parte confiável com reconhecimento de declarações manualmente

Para adicionar uma nova relação de confiança de terceira parte confiável usando o snap-in de gerenciamento de AD FS \- e configurar manualmente as configurações, execute o procedimento a seguir em um servidor de Federação.

A associação em **Administradores**, ou equivalente, no computador local é o mínimo necessário para concluir este procedimento.  Examine os detalhes sobre como usar as contas apropriadas e as associações de grupo em [grupos padrão e de domínio](https://go.microsoft.com/fwlink/?LinkId=83477).

1. No Gerenciador do Servidor, clique em **Ferramentas** e depois selecione **Gerenciamento do AD FS**.

2. Em **ações**, clique em **Adicionar confiança de terceira parte confiável**.

    ![Captura de tela da caixa de diálogo AD FS com a opção Adicionar confiança de terceira parte confiável no painel Ações chamado.](media/Create-a-Relying-Party-Trust/addtrust1.PNG)

3. Na página **Boas-vindas**, escolha **Reconhecimento de declaração** e clique em **Iniciar**.

    ![Captura de tela da página inicial do assistente Adicionar confiança de terceira parte confiável mostrando a opção de reconhecimento de declarações selecionada.](media/Create-a-Relying-Party-Trust/addtrust2.PNG)

4. Na página **Selecionar Fonte de Dados**, clique em **Inserir manualmente dados sobre a terceira parte confiável** e clique em **Avançar**.

    ![Captura de tela da página selecionar fonte de dados do assistente Adicionar confiança de terceira parte confiável mostrando a opção inserir dados sobre a terceira parte confiável manualmente selecionada.](media/Create-a-Relying-Party-Trust/addtrust3.PNG)

5. Na página **Especificar Nome de Exibição**, digite um nome em **Nome de exibição**, em **Notas** digite uma descrição para essa terceira parte confiável e, em seguida, clique em **Avançar**.

    ![Captura de tela da página Especificar nome de exibição do assistente para adicionar confiança de terceira parte confiável.](media/Create-a-Relying-Party-Trust/addtrust4.PNG)

6. Na página **Configurar certificado** , se você tiver um certificado de criptografia de token opcional, clique em **procurar** para localizar um arquivo de certificado e, em seguida, clique em **Avançar**.

    ![Captura de tela da página Configurar certificado do assistente Adicionar confiança de terceira parte confiável mostrando o botão de procura chamado.](media/Create-a-Relying-Party-Trust/addtrust5.PNG)

7. Na página **Configurar URL** , execute um ou ambos os procedimentos a seguir, clique em **Avançar** e vá para a etapa 8:

    - Marque a caixa de seleção **habilitar suporte para o \- protocolo passivo do WS Federation** . Em **\- URL do protocolo passivo WS Federation de terceira parte confiável**, digite a URL para essa terceira parte confiável e clique em **Avançar**.

    - Marque a caixa de seleção **Habilitar suporte para o protocolo WebSSO do SAML 2.0** . Em **URL do serviço de SSO do saml 2,0 de terceira parte confiável**, digite o Security Assertion Markup Language \( \) URL do ponto de extremidade do serviço SAML para essa terceira parte confiável e clique em **Avançar**.

    ![Captura de tela da página Configurar certificado do assistente Adicionar confiança de terceira parte confiável mostrando a configuração explicada acima.](media/Create-a-Relying-Party-Trust/addtrust6.PNG)

8. Na página **Configurar Identificadores**, especifique um ou mais identificadores da terceira parte confiável, clique em **Adicionar** para adicioná-los à lista e clique em **Avançar**.

    ![Captura de tela da página Configurar identificadores do assistente Adicionar confiança de terceira parte confiável mostrando identificadores adicionados à seção de identificadores de confiança de terceira parte confiável.](media/Create-a-Relying-Party-Trust/addtrust8.PNG)

9. Em **Escolher Política de Controle de Acesso**, escolha uma política e clique em **Avançar**.  Para obter mais informações sobre políticas de controle de acesso, consulte [políticas de controle de acesso em AD FS](Access-Control-Policies-in-AD-FS.md).

    ![Captura de tela da página escolher política de controle de acesso do assistente Adicionar confiança de terceira parte confiável mostrando a opção permitir todos e exigir MFA realçada.](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. Na página **Pronto para adicionar confiança**, revise as configurações e clique em **Avançar** para salvar as informações do objeto de confiança de terceira parte confiável.

    ![Captura de tela da página pronto para adicionar confiança do assistente Adicionar confiança de terceira parte confiável.](media/Create-a-Relying-Party-Trust/addtrust10.PNG)

11. Na página **Concluir**, clique em **Fechar**. Essa ação exibe automaticamente a caixa de diálogo **Editar Regras de Declaração**.

    ![Captura de tela da página concluir do assistente Adicionar confiança de terceira parte confiável.](media/Create-a-Relying-Party-Trust/addtrust11.PNG)

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>Para criar um confiança de terceira parte confiável com reconhecimento de declarações usando metadados de Federação

Para adicionar uma nova relação de confiança de terceira parte confiável, usando o snap-in de gerenciamento de AD FS, importando automaticamente os dados de configuração sobre o parceiro de metadados de Federação que o parceiro publicou em uma rede local ou com a Internet, execute o procedimento a seguir em um servidor de Federação na organização do parceiro de conta.

>[!NOTE]
>Embora tenha sido uma prática comum usar certificados com nomes de host não qualificados como https://myserver , esses certificados não têm nenhum valor de segurança e podem permitir que um invasor represente um serviço de Federação que esteja publicando metadados de Federação. Portanto, ao consultar metadados de Federação, você deve usar apenas um nome de domínio totalmente qualificado, como https://myserver.contoso.com .

A associação em **Administradores**, ou equivalente, no computador local é o mínimo necessário para concluir este procedimento.  Examine os detalhes sobre como usar as contas apropriadas e as associações de grupo em [grupos padrão e de domínio](https://go.microsoft.com/fwlink/?LinkId=83477).

1. No Gerenciador do Servidor, clique em **Ferramentas** e depois selecione **Gerenciamento do AD FS**.

2. Em **ações**, clique em **Adicionar confiança de terceira parte confiável**.

    ![Outra captura de tela da caixa de diálogo AD FS com a opção Adicionar confiança de terceira parte confiável no painel Ações é chamada de saída.](media/Create-a-Relying-Party-Trust/addtrust1.PNG)

3. Na página **Boas-vindas**, escolha **Reconhecimento de declaração** e clique em **Iniciar**.

    ![Outra captura de tela da página inicial do assistente Adicionar confiança de terceira parte confiável mostrando a opção de reconhecimento de declarações selecionada.](media/Create-a-Relying-Party-Trust/addtrust2.PNG)

4. Na página **Selecionar Fonte de Dados**, clique em **Importar dados sobre a terceira parte confiável publicados online ou em uma rede local**. Em **Endereço dos metadados de federação (nome do host ou URL)**, digite a URL de metadados de federação ou o nome do host do parceiro. Em seguida, clique em **Avançar**.

    ![Captura de tela da página selecionar fonte de dados do assistente Adicionar confiança de terceira parte confiável mostrando a opção importar dados sobre a terceira parte confiável publicada online ou em uma rede local selecionada.](media/Create-a-Relying-Party-Trust/addtrust12.PNG)

5. Na página Especificar nome de exibição, digite um nome em **nome para exibição**, em observações, digite uma descrição para a terceira parte confiável e clique em **Avançar**.

6. Na página Escolher Regras de Autorização de Emissão , selecione **Permitir que todos os usuários acessem esta terceira parte confiável** ou **Negar a todos os usuários o acesso a esta terceira parte confiável** e clique em **Avançar**.

7. Na página Pronto para Adicionar Objeto de Confiança, examine as configurações e, em seguida, clique em **Avançar** para salvar as informações de seu objeto de confiança de terceira parte confiável.

8. Na página Concluir , clique em **Fechar**. Essa ação exibe automaticamente a caixa de diálogo Editar Regras de Declaração. Para obter mais informações sobre como proceder ao adicionar regras de declaração a esse objeto de confiança de terceira parte confiável, consulte as Referências adicionais.




## <a name="see-also"></a>Consulte Também
[Operações do AD FS](../ad-fs-operations.md)
