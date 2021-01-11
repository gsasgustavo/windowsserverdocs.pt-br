---
title: Atualizações expressas para o Windows Server 2016 ativadas novamente para a atualização de novembro de 2018
description: Fornece informações sobre as Atualizações expressas no Windows Server 2016
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 08/07/2020
ms.openlocfilehash: e35f2d8c80ab31f85dc16d3b8f9b37af3ed105ed
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950312"
---
# <a name="express-updates-for-windows-server-2016-re-enabled-for-november-2018-update"></a>Atualizações expressas para o Windows Server 2016 ativadas novamente para a atualização de novembro de 2018

> Aplica-se a: Windows Server 2016

Nas atualizações das terças-feiras de 13 de novembro de 2018 em diante, o Windows publicará as Atualizações expressas novamente para o Windows Server 2016. As Atualizações expressas do Windows Server 2016 foram interrompidas em meados de 2017, depois que foi encontrado um problema significativo que impedia que as atualizações fossem instaladas corretamente. Embora o problema foi corrigido em novembro de 2017, a equipe de atualização adotou uma abordagem conservadora para publicação dos pacotes expressos para garantir que a maioria dos clientes teria a atualização de 14 de novembro de 2017 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) instalada em seu ambientes de servidores e não seriam afetados pelo problema.

Os administradores de sistema do WSUS e do Configuration Manager precisam estar cientes de que em novembro de 2018, mais uma vez, terão dois pacotes para a atualização do Windows Server 2016: uma atualização completa e uma atualização expressa. Os administradores de sistema que desejam usar a expressa em seus ambientes de servidor precisam confirmar que o dispositivo recebeu uma atualização completa desde 14 de novembro de 2017 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) para garantir que a instalação expressa seja instalada corretamente. Qualquer dispositivo que não foi atualizado desde a atualização de 14 de novembro de 2017 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) verão falhas repetidas que consomem largura de banda e recursos de CPU em um loop infinito, caso seja tentado realizar a atualização expressa.  A correção para esse estado seria o administrador do sistema interromper o envio por push da atualização expressa e enviar por push uma atualização completa recente para interromper o loop de falha.

Em 13 de novembro de 2018, os clientes de atualização expressa verão uma redução imediata de tamanho de pacote entre o seu sistema de gerenciamento e os pontos de extremidade do Windows Server 2016.