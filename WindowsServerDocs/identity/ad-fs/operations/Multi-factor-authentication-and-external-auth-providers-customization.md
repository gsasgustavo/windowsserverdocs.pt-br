---
description: 'Saiba mais sobre: personalização de autenticação multifator e provedores de autenticação externa'
title: Personalização de autenticação multifator e provedores de autenticação externa
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.openlocfilehash: 5f05abf8c14fc3829fe9a0e99ef12de2cde97f81
ms.sourcegitcommit: 6a62d736e4d9989515c6df85e2577662deb042b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98103718"
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>Personalização de autenticação multifator e provedores de autenticação externa

No AD FS, o suporte para autenticação multifator é fornecido prontos para uso \- \- \- . Por exemplo, você pode configurar AD FS para usar a \- autenticação de certificado interna como a autenticação do segundo fator. Você também pode usar provedores de autenticação externa. Essa abordagem pode permitir a integração de AD FS com serviços adicionais, como a autenticação multifator do Azure, ou você pode desenvolver seu próprio provedor. Consulte o [Guia de solução: gerenciar riscos com o \- controle de acesso de vários fatores](./manage-risk-with-conditional-access-control.md) para obter mais informações sobre como registrar o provedor de autenticação externa usando AD FS.

Recomendamos que um provedor de autenticação externo use as classes definidas no arquivo. CSS que AD FS fornece para criar a interface do usuário de autenticação. Você pode usar o seguinte cmdlet para exportar o tema da Web padrão e inspecionar as classes de interface do usuário e os elementos definidos no arquivo .css. O arquivo. CSS pode ser usado no desenvolvimento da \- interface do usuário de entrada de um provedor de autenticação externo.

```powershell
Export-AdfsWebTheme -Name default -DirectoryPath C:\theme
```

Veja a seguir um exemplo da interface do \- usuário de entrada, que é realçada em vermelho, por um provedor de autenticação externa. A interface do usuário usa as classes de IU no arquivo AD FS. css.

![Captura de tela que mostra um exemplo da interface do usuário de entrada.](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)

Antes de escrever um novo método de autenticação personalizado, recomendamos que você estude as definições AD FS tema e estilo para entender os requisitos de criação de conteúdo.

-   Um método de autenticação personalizado somente cria um segmento HTML na página de entrada AD FS \- e não na página inteira. Você deve usar a definição de estilo do AD FS para obter a aparência e o comportamento consistentes.

![AD FS e MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)

-   Lembre-se de que AD FS administradores podem personalizar os estilos de AD FS. . Não recomendamos codificar seus estilos próprios. Em vez disso, é recomendável usar estilos de AD FS sempre que possível.

-   Prontos \- \- para uso, AD FS estilos são criados com um \- estilo de EPD da esquerda para a \- direita \( \) e um direito \- à \- esquerda \( DPE \) . Os administradores podem personalizar ambos e podem fornecer \- estilos específicos de idioma por meio da definição de tema da Web. Cada folha de estilo possui três seções com os respectivos comentários:

    -   **estilos** \- de tema Esses estilos não devem e não podem ser usados. Esses estilos são destinados a definir o tema em todas as páginas. Eles são definidos por um ID de elemento intencionalmente, de forma que nunca sejam reutilizados.

    -   **estilos comuns** \- Esses são os estilos que devem ser usados para seu conteúdo.

    -   estilos de fator de **forma** \- Esses são estilos para diferentes fatores forma. Você deve compreender esta seção para assegurar que seu conteúdo funcione com diferentes fatores forma, por exemplo, telefones e tablets.

Para obter informações adicionais, consulte o [Guia de solução: gerenciar riscos com o \- controle de acesso de vários fatores](./manage-risk-with-conditional-access-control.md) e [Guia de solução: gerenciar riscos com a \- autenticação multifator adicional para aplicativos confidenciais](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx).

## <a name="additional-references"></a>Referências adicionais
[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
