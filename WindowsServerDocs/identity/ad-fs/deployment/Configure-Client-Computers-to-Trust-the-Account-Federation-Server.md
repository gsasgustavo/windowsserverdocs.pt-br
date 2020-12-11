---
description: 'Saiba mais sobre: configurar computadores cliente para confiar no servidor de Federação da conta'
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: Configurar computadores cliente para confiar no servidor de Federação da conta
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 9b76fd4bd7ae09e9940dc7501136c5b0bb3449f6
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97050294"
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>Configurar computadores cliente para confiar no servidor de Federação da conta

Para que os computadores cliente possam acessar com êxito os aplicativos federados usando Serviços de Federação do Active Directory (AD FS) \( AD FS \) , você deve primeiro definir as configurações do Internet Explorer em cada computador cliente para que o navegador confie no servidor de Federação da conta. Você pode fazer isso manualmente ou por meio de Política de Grupo, dependendo da sua preferência administrativa, concluindo um dos procedimentos a seguir.

## <a name="configuring-internet-explorer-settings-manually"></a>Definindo manualmente as configurações do Internet Explorer
Você pode usar o procedimento a seguir para definir manualmente as configurações do Internet Explorer de cada usuário para dar suporte à Federação por meio de AD FS. Se vários usuários usarem um único computador, conclua esse procedimento várias vezes — uma vez para cada perfil de usuário.

Para executar esse procedimento, faça logon como o usuário que acessará aplicativos federados. Essa é uma \- configuração específica de perfil. Portanto, é necessário adicionar manualmente essa configuração para cada perfil existente em um computador específico.

#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>Para configurar manualmente os computadores cliente para confiar no servidor de Federação da conta

1.  No computador cliente, inicie o Internet Explorer.

2.  No menu **ferramentas** , clique em **Opções da Internet**.

3.  Na guia **segurança** , clique no ícone **intranet local** e, em seguida, clique em **sites**.

4.  Clique em **avançado** e, em **Adicionar este site à zona**, digite o \( nome DNS completo do sistema de nome de domínio \) do servidor de Federação da conta \( , por exemplo, https: \/ \/ FS1.fabrikam.com \) e clique em **Adicionar**.

5.  Clique em **OK** três vezes.

## <a name="configuring-internet-explorer-settings-by-using-group-policy"></a>Definindo as configurações do Internet Explorer usando Política de Grupo
Para a maioria das implantações, recomendamos que você use Política de Grupo para enviar por push as configurações apropriadas do Internet Explorer para cada computador cliente.

A associação em **Administradores de domínio** ou administradores de **empresa**, ou equivalente, em Active Directory Domain Services \( AD DS \) é o mínimo necessário para concluir este procedimento.  Examinar os detalhes sobre como usar as contas apropriadas e as associações de grupo em [grupos padrão e de domínio](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.Microsoft.com \/ fwlink \/ ? LinkId \= 83477 \) .

#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-group-policy"></a>Para configurar computadores cliente para confiar no servidor de Federação da conta usando Política de Grupo

1.  Em um controlador de domínio na floresta da organização do parceiro de conta, inicie o snap-in de **Gerenciamento de política de grupo** \- .

2.  Localize o GPO do objeto Política de Grupo apropriado \( \) , clique com o botão direito do mouse \- nele e clique em **Editar**.

3.  Na árvore de console, abra **preferências de configuração do usuário \\ \\ configurações do Windows \\ manutenção do Internet Explorer** e clique em **segurança**.

4.  No painel de detalhes, clique duas vezes \- em **zonas de segurança e classificações de conteúdo**.

5.  Em **zonas de segurança e privacidade**, clique em **importar as configurações de privacidade e zonas de segurança atuais** e clique em **Modificar configurações**.

6.  Clique em **intranet local** e em **sites**.

7.  Em **Adicionar este site à zona**, digite o nome DNS completo do servidor de Federação de conta \( , por exemplo, https: \/ \/ FS1.fabrikam.com \) , clique em **Adicionar** e, em seguida, clique em **fechar**.

8.  Clique em **OK** duas vezes para aplicar essas alterações ao política de grupo.

