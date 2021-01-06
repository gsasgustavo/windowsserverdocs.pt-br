---
title: Modelos NPS
description: Este tópico fornece uma visão geral dos modelos de servidor de políticas de rede no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 66fb4d0b7d2fc5bd77fb1b943b45a8c75408866e
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947442"
---
# <a name="nps-templates"></a>Modelos NPS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

\(Os modelos NPS do servidor \) de políticas de rede permitem que você crie elementos de configuração, como serviço RADIUS \( \) clientes RADIUS ou segredos compartilhados, que você pode reutilizar no NPS local e exportar para uso em outros NPSs.

Os modelos de NPS são projetados para reduzir a quantidade de tempo e o custo necessário para configurar o NPS em um ou mais servidores. Os seguintes tipos de modelo de NPS estão disponíveis para configuração no gerenciamento de modelos:

- Segredos compartilhados
- Clientes RADIUS
- Servidores RADIUS remotos
- Filtros de IP
- Grupos de servidores de atualizações

Configurar um modelo é diferente de configurar diretamente o NPS. A criação de um modelo não afeta a funcionalidade do NPS. Somente quando você seleciona o modelo no local apropriado no console do NPS, o modelo afeta a funcionalidade do NPS.

Por exemplo, se você configurar um cliente RADIUS no console do NPS em clientes e servidores RADIUS, você alterou a configuração do NPS e fez uma etapa na configuração do NPS para se comunicar com um dos seus servidores de acesso à rede \( nas \) . \(A próxima etapa seria configurar o NAS para se comunicar com o NPS. \) No entanto, se você configurar um novo modelo de clientes RADIUS no console do NPS em **Gerenciamento de modelos** , em vez de criar um novo cliente RADIUS em **clientes e servidores RADIUS**, você criou um modelo, mas ainda não alterou a funcionalidade do NPS. Para alterar a funcionalidade do NPS, você deve selecionar o modelo do local correto no console do NPS.

## <a name="creating-templates"></a>Como criar modelos

Para criar um modelo, abra o console do NPS, clique com o botão direito do mouse em um tipo de modelo, como **filtros de IP** e clique em **novo**. Uma nova caixa de diálogo Propriedades do modelo é aberta e permite que você configure seu modelo.

## <a name="using-templates-locally"></a>Usando modelos localmente

Você pode usar um modelo que você criou no **Gerenciamento de modelos** navegando até um local no console do NPS onde o modelo pode ser aplicado. Por exemplo, se você criar um novo modelo de segredos compartilhados que deseja aplicar a uma configuração de cliente RADIUS, em **clientes RADIUS e servidores** e **clientes RADIUS**, abra as propriedades do cliente RADIUS. Em **selecionar um modelo de segredos compartilhados existente**, selecione o modelo que você criou anteriormente na lista de modelos disponíveis.

Para obter mais informações sobre o NPS, consulte [servidor de diretivas de rede (NPS)](nps-top.md).
