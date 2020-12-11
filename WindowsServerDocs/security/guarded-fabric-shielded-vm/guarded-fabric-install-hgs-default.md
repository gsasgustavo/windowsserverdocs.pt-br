---
description: 'Saiba mais sobre: instalar o HGS em uma nova floresta'
title: Instalar o HGS em uma nova floresta
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 934efb699dd1c9f37219606ebc7f1b748f61eb18
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049724"
---
# <a name="install-hgs-in-a-new-forest"></a>Instalar o HGS em uma nova floresta

>Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016

## <a name="add-the-hgs-server-role"></a>Adicionar a função de servidor HGS

Execute os seguintes comandos em uma sessão do PowerShell com privilégios elevados para adicionar a função de servidor HGS e instalar o HGS.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)]

## <a name="install-hgs"></a>Instalar o HGS

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)]

## <a name="next-steps"></a>Próximas etapas

- Para as próximas etapas para configurar o atestado baseado em TPM, consulte [inicializar o cluster HgS usando o modo TPM em uma nova floresta dedicada (padrão)](guarded-fabric-initialize-hgs-tpm-mode-default.md).
- Para as próximas etapas para configurar o atestado de chave de host, consulte [inicializar o cluster HgS usando o modo de chave em uma nova floresta dedicada (padrão)](guarded-fabric-initialize-hgs-key-mode-default.md).
- Para as próximas etapas para configurar o atestado baseado em administrador (preterido no Windows Server 2019), consulte [inicializar o cluster HgS usando o modo ad em uma nova floresta dedicada (padrão)](guarded-fabric-initialize-hgs-ad-mode-default.md).

## <a name="next-step"></a>Próxima etapa

> [!div class="nextstepaction"]
> [Iniciar o HGS](guarded-fabric-initialize-hgs.md)


