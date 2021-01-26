---
title: AD FS entrada paginada
description: Este documento descreve a nova experiência de entrada para o AD FS 2019.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.openlocfilehash: f7918c6b6a0ee4f5efb9da45d722f5c49dcc9f42
ms.sourcegitcommit: 6717decb5839aa340c81811d6fde020aabaddb3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98781862"
---
# <a name="ad-fs-paginated-sign-in"></a>AD FS entrada paginada


Para AD FS no Windows Server 2019, reprojetamos a interface do usuário de entrada.  Agora, a entrada AD FS terá a mesma aparência do Azure AD.  Isso fornece aos usuários uma experiência de entrada mais consistente, incorporando um fluxo de usuário centralizado e paginado.

## <a name="whats-changing"></a>O que está mudando
Em AD FS no Windows Server 2012 R2 e 2016, sua tela de entrada se parece com esta:

![Captura da tela de entrada antiga.](media/AD-FS-paginated-sign-in/signin1.png)

Estamos afastando da exibição de um único Formulário localizado no lado direito da tela.

Em AD FS no Windows Server 2019, essas são as principais alterações de design que você verá:


- **Uma interface do usuário centralizada**. Anteriormente, a interface do usuário de entrada existia no lado direito da tela, como mostrado acima. Mudamos a frente e a central da interface do usuário para modernizar a experiência.
- **Paginação**. Em vez de fornecer um longo formato a ser preenchido, incorporamos um novo fluxo que o guiará pela experiência de entrada passo a passo. Nossa telemetria mostra que, com essa abordagem, nossos clientes têm entradas mais bem-sucedidas. Ele também fornece mais flexibilidade para incorporar vários métodos de autenticação, como a autenticação de fator de telefone dos EUA.

![Captura de tela da nova entrada de conexão.](media/AD-FS-paginated-sign-in/signin2.png)

Na primeira página, você será solicitado a inserir seu nome de usuário. Você também pode selecionar a opção "Mantenha-me conectado" para reduzir a frequência de prompts de entrada e permanecer conectado quando for seguro fazê-lo. (Essa opção está desabilitada por padrão.)

![Captura de tela da primeira página do novo logon.](media/AD-FS-paginated-sign-in/signin3.png)

Na segunda página, você verá as opções de autenticação, configuradas pelo administrador. Se permitir a autenticação externa como primário estiver habilitado, isso também será incluído.

![Captura de tela da segunda página do novo botão entrar.](media/AD-FS-paginated-sign-in/signin4.png)

Na terceira página, você será solicitado a inserir sua senha (supondo que você selecionou "senha" como a opção de autenticação).

## <a name="how-to-get-the-new-experience"></a>Como obter a nova experiência

### <a name="new-installation-of-ad-fs"></a>Nova instalação do AD FS
Se você for um novo cliente para AD FS, você receberá o novo design por padrão.

### <a name="upgrading-a-farm"></a>Atualizando um farm
Se você for um cliente existente AD FS 2012 R2 ou 2016, há duas maneiras de receber o novo design depois de atualizar os servidores para AD FS 2019 e habilitar o FBL para 2019.

- Permitir a nova entrada por meio do PowerShell. Execute o seguinte comando para habilitar a paginação: ``Set-AdfsGlobalAuthenticationPolicy -EnablePaginatedAuthenticationPages $true``

 - Habilite a autenticação externa como primária, seja por meio do PowerShell ou pelo Gerenciador do Servidor de AD FS. As novas páginas de entrada paginadas serão habilitadas quando esse recurso estiver habilitado.
Se você for um novo cliente para AD FS, você receberá o novo design por padrão. No entanto, se você for um cliente existente com AD FS 2012 R2 ou 2016, haverá várias etapas que você precisará tomar para receber o novo design: ``Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true``

## <a name="customization"></a>Personalização
As opções de personalização ainda serão aplicáveis para o AD FS 2019.
Abaixo estão alguns links para outros documentos para sua referência.

• Para aqueles que não planejam atualizar seus servidores para AD FS 2019, mas ainda desejam o novo design: [usando um tema da Web do Azure ad UX no serviços de Federação do Active Directory (AD FS)](azure-ux-web-theme-in-ad-fs.md)

• Um local central para personalização: [AD FS personalização de entrada do usuário](ad-fs-user-sign-in-customization.md)
