---
title: Instalar ou Remover Pacotes de Idiomas
description: Saiba como instalar ou remover pacotes de idiomas no Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 98f13f63-4480-40ba-a7ef-d1d9b7582e5f
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 7dcbc6cb67c79d59dd589ae9b8747e4319967731
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755392"
---
# <a name="install-or-remove-language-packs"></a>Instalar ou Remover Pacotes de Idiomas

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

> [!NOTE]
>  Você deve primeiro criar uma imagem multilíngue do Windows, conforme descrito nos [pacotes de idiomas e a implantação](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824829(v=win.10)) , antes de adicionar o pacote de idiomas do Windows Server Essentials.

 Os pacotes de idiomas estão disponíveis somente para a criação de imagens em vários idiomas. As informações contidas nesta seção são específicas para instalar ou remover pacotes de idiomas no Windows Server Essentials.

> [!NOTE]
>  Se você pretende executar a IC (Configuração Inicial) em um computador cliente que não seja compatível com idiomas do leste asiático, como ja-jp, e se inglês não estiver incluído na imagem multilíngue no servidor, a página da Web da IC exibirá quadrados. Para a página da Web da IC assumir inglês como padrão, a imagem multilíngue criada deve incluir inglês.

## <a name="adding-language-packs-to-an-image"></a>Adicionando pacotes de idiomas a uma imagem
 Os pacotes de idiomas estão disponíveis no DVD de personalização de OEM. Recomenda-se copiar os pacotes de idiomas ao computador do técnico antes de adicionar os pacotes de idiomas à imagem.

 É necessário usar o comando a seguir para instalar pacotes de idiomas:

 **dism.exe/Online/Add-Package/PackagePath: C: \\<caminho completo do diretório de arquivos cab \>\lp.cab**

 Por exemplo, o comando a seguir mostra como adicionar um pacote do idioma alemão:

 **dism.exe /online /Add-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**

> [!IMPORTANT]
>  Você também deve aplicar pacotes de idiomas para o Windows Server Essentials para localizar o sistema operacional por completo.

## <a name="removing-language-packs-from-an-image"></a>Removendo pacotes de idiomas a partir de uma imagem
 Você pode usar o comando a seguir para remover um pacote de idioma que você não deseja mais incluir em uma imagem:

 **dism.exe/online/Remove-Package/PackagePath: C: \\<caminho completo para o diretório de arquivos cab \>\lp.cab**

 Por exemplo, o comando a seguir mostra como remover um pacote do idioma alemão:

 **dism.exe /online /Remove-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**

## <a name="see-also"></a>Consulte Também

 [Criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para](Preparing-the-Image-for-Deployment.md) [testar a implantação da experiência do cliente](Testing-the-Customer-Experience.md)