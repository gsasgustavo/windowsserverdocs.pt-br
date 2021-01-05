---
title: Testando a Experiência do Usuário
description: Saiba como executar a configuração inicial de um computador de destino para verificar a experiência do cliente e verificar as personalizações do parceiro.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 1b1a2040-4cfd-48bf-8d04-3ffde9c26b9b
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: afe9ec09266eb57c25b0dea158a434da200573b5
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755342"
---
# <a name="testing-the-customer-experience"></a>Testando a Experiência do Usuário

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Para verificar a experiência do usuário e suas personalizações de parceiro, percorra a Configuração Inicial de um computador de destino. Recomenda-se que você conclua a Configuração Inicial ao menos uma vez manualmente para passar pela experiência do usuário. Se você fez uma parceria entre as marcas do Dashboard, é necessário concluir a Configuração Inicial para verificar a identidade visual. Se você comarcar o site de Acesso via Web remoto, deverá acessar o http://<ServerName \> para verificar a identidade visual (<ServerName \> é o nome do servidor). Você pode usar a seção Configuração Inicial do arquivo cfg.ini para automatizar o teste da experiência do usuário. Para obter mais informações sobre a criação dessa seção no arquivo cfg.ini, consulte [Criar o Arquivo Cfg.ini](Create-the-Cfg.ini-File.md).

> [!IMPORTANT]
>  Execute o comando Sysprep.exe para preparar a imagem para implantação antes de testar a experiência da Configuração Inicial. Para obter mais informações sobre a execução do Sysprep.exe, consulte [Preparando a Imagem para Implantação](Preparing-the-Image-for-Deployment.md).

> [!IMPORTANT]
>  Para testar a Configuração Inicial, é necessária uma conexão de rede. O DHCP não está configurado ou instalado no servidor, o que possibilita o teste da rede sem interferência.

 Para verificar as Informações de Suporte de parceiro, no Dashboard, clique na seta para baixo ao lado do botão Ajuda.

## <a name="see-also"></a>Consulte Também
 [Criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para implantação](Preparing-the-Image-for-Deployment.md)