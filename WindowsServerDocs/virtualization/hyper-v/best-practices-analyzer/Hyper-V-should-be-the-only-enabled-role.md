---
title: O Hyper-V deve ser a única função habilitada
description: Saiba o que fazer quando as funções que não sejam o Hyper-V estiverem habilitadas no servidor.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 5a0ed176-048f-40b1-b56c-8391b805fd37
ms.date: 8/16/2016
ms.openlocfilehash: f575f981975253faea30dad610120f3e314a1edf
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97833611"
---
# <a name="hyper-v-should-be-the-only-enabled-role"></a>O Hyper-V deve ser a única função habilitada

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, consulte [Analisador de Práticas Recomendadas](https://go.microsoft.com/fwlink/?LinkId=122786).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema

*Funções diferentes do Hyper-V estão habilitadas neste servidor.*

Na maioria dos casos, não é uma boa ideia instalar outras funções em um servidor que executa a função Hyper-V. Host de Virtualização de Área de Trabalho Remota serviço de função é uma exceção, porque faz parte da função de Serviços de Área de Trabalho Remota e requer que o Hyper-V seja instalado no mesmo servidor.

## <a name="impact"></a>Impacto

*A função Hyper-V deve ser a única função habilitada em um servidor.*

Essa prática recomendada ajuda a manter o sistema operacional do host livre de funções, recursos e aplicativos que não são necessários para executar o Hyper-V. Seguir essa prática recomendada e executar o Hyper-V no nano Server ajuda a reduzir o número de atualizações necessárias porque apenas o nano Server, os componentes do serviço Hyper-V e o hipervisor do Windows estão sujeitos a atualizações de software.

## <a name="resolution"></a>Resolução

*Use Gerenciador do Servidor para remover todas as funções, exceto Hyper-V.*

Gerenciador do Servidor inclui o assistente para remover funções. Este assistente permite remover mais de uma função de uma vez. Antes de remover as funções, o assistente para remover funções verifica as dependências para reduzir o risco de remover o software do qual outras funções dependem. Se forem encontradas dependências, o assistente solicitará que você aprove a remoção de outras funções, serviços de função ou software exigido pelas funções instaladas.

Para usar Gerenciador do Servidor, você deve estar conectado ao computador como administrador.

#### <a name="to-remove-a-role"></a>Para remover uma função

1.  Abra Gerenciador do Servidor usando atalhos no menu **Iniciar** , na barra de tarefas do Windows ou em ferramentas administrativas.
2.   Na área **Resumo de funções** da janela principal do Gerenciador do servidor, clique em **remover funções**. Siga as instruções no Assistente para remover a função.





