---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: Implantar o AD DS em uma organização com o Windows 2000
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 664224168efd347e6ca391112bf6b838d1f1c29a
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88938826"
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Implantar o AD DS em uma organização com o Windows 2000

> Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Se sua organização estiver executando o Windows 2000 Active Directory, você poderá implantar o Windows Server 2008 Active Directory Domain Services (AD DS) executando uma atualização in-loco de alguns ou de todos os sistemas operacionais dos controladores de domínio para o Windows Server 2008 ou introduzindo os controladores de domínio que executam o Windows Server 2008 em seu ambiente.

Antes de adicionar um controlador de domínio executando o Windows Server 2008 a um domínio existente do Windows 2000 Active Directory, você deve executar **adprep**, uma ferramenta de linha de comando. A adprep estende o esquema de AD DS, atualiza os descritores de segurança padrão dos objetos selecionados e adiciona novos objetos de diretório conforme exigido por alguns aplicativos. A Adprep está disponível no disco de instalação do Windows Server 2008 (\sources\adprep\adprep.exe). Para obter mais informações, consulte [adprep](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731728(v=ws.11)).

> [!NOTE]
> Se você quiser executar uma atualização in-loco de um controlador de domínio existente do Windows 2000 AD DS para o Windows Server 2008, você deve primeiro atualizar o servidor para o Windows Server 2003 e, em seguida, atualizá-lo para o Windows Server 2008.

A ilustração a seguir mostra as etapas para implantar o Windows Server 2008 AD DS em um ambiente de rede que está atualmente executando o Windows 2000 Active Directory.

![Implantando em uma organização do Windows 2000](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)

> [!NOTE]
> Se você quiser definir o nível funcional de domínio ou floresta para o Windows Server 2008, todos os controladores de domínio em seu ambiente devem executar o sistema operacional Windows Server 2008.

Consolidar domínios de recursos e contas que são atualizados no lugar de um ambiente do Windows 2000 como parte do seu Windows Server 2008 AD DS implantação pode exigir a reestruturação de domínio entre florestas ou intraflorestal. A reestruturação de AD DS domínios entre florestas ajuda a reduzir a complexidade de sua organização e os custos administrativos associados. A reestruturação de AD DS domínios em uma floresta ajuda a diminuir a sobrecarga administrativa para sua organização, reduzindo o tráfego de replicação, reduzindo a quantidade de administração de usuários e grupos necessária e simplificando a administração do Política de Grupo. Para obter mais informações, consulte [Guia de ADMT: migrando e Reestruturando Active Directory domínios](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc974332(v=ws.10)).

Para obter uma lista de tarefas detalhadas que você pode usar para planejar e implantar AD DS em uma organização que está executando o Windows 2000 Active Directory, consulte [lista de verificação: Implantando AD DS em uma organização do windows 2000](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc732737(v=ws.10)).
