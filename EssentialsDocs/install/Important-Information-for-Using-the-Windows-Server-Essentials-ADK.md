---
title: Informações importantes para a utilização do Windows Server Essentials ADK
description: Saiba mais sobre as diferenças importantes entre o Windows 8 ADK e o Windows Server Essentials ADK.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 26cb2992-1250-4672-98ee-8b870baa45d5
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 36cdbc03f6b241026f24c811cb69d5331f71bae7
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755052"
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Informações importantes para a utilização do Windows Server Essentials ADK

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Para criar e personalizar uma imagem do Windows Server Essentials, você usa muitas das ferramentas do [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248647), mas há algumas diferenças importantes entre o Windows 8 ADK e o Windows Server Essentials ADK.

 Você deve estar ciente das seguintes diferenças importantes:

-   Algumas configurações foram alteradas em  **%windir%\setup\script\SetupComplete.cmd**. Se você quiser usar esse comando, poderá adicionar outras `cmdlines` , mas não remover as linhas existentes.

## <a name="working-with-passwords"></a>Trabalhando com senhas

-   A senha de administrador é definida como Admin@123 e o logon automático é habilitado no Install.wim\unattend.xml. Portanto, não é preciso redigitar a senha várias vezes durante a configuração inicial do servidor. Se você tiver um unattend.xml personalizado na raiz da mídia removível, essas configurações serão substituídas e você precisará definir a senha e o logon durante a inicialização.

-   Durante a Configuração Inicial, o usuário final é solicitado a criar uma nova conta e senha. Essa nova conta se torna a conta de administrador de rede para o sistema operacional. A conta de Administrador e o logon automático então são desabilitados. Você poderá automatizar esse processo usando o arquivo cfg.ini para testar a garantia de qualidade.

-   Consulte a documentação do [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) para obter detalhes sobre a criação de um arquivo unattend.xml.

## <a name="see-also"></a>Consulte Também

 [Introdução com o Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) [criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para](Preparing-the-Image-for-Deployment.md) [testar a implantação da experiência do cliente](Testing-the-Customer-Experience.md)

