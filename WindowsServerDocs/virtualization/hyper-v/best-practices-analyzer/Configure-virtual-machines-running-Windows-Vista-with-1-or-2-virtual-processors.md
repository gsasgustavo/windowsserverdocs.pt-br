---
title: Configurar máquinas virtuais que executam o Windows Vista com 1 ou 2 processadores virtuais
description: Saiba o que fazer quando uma máquina virtual que executa o Windows Vista estiver configurada com mais de 2 processadores virtuais.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: e562bce3-fd68-42c9-821c-12022ae4746c
ms.date: 8/16/2016
ms.openlocfilehash: 3e49a55ed27d62fa955800867a7a4e3c9dacf319
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846410"
---
# <a name="configure-virtual-machines-running-windows-vista-with-1-or-2-virtual-processors"></a>Configurar máquinas virtuais que executam o Windows Vista com 1 ou 2 processadores virtuais

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Configuração|
|**Categoria**|Erro|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema

*Uma máquina virtual que executa o Windows Vista está configurada com mais de 2 processadores virtuais.*

## <a name="impact"></a>Impacto

*A Microsoft não oferece suporte à configuração das seguintes máquinas virtuais:*

\<list of virtual machine names>

## <a name="resolution"></a>Resolução

*Desligue a máquina virtual e remova um ou mais processadores virtuais.*

### <a name="to-remove-virtual-processors"></a>Para remover processadores virtuais

1.  Abra o Gerenciador do Hyper-V. Clique em **Iniciar**, vá em **Ferramentas Administrativas** e clique em **Gerenciador do Hyper-V**.

2.  No painel de resultados, em **máquinas virtuais**, selecione a máquina virtual que você deseja configurar. O estado da máquina virtual deve ser listado como **desativado**. Se não estiver, clique com o botão direito do mouse na máquina virtual e clique em **desligar**.

3.  No painel **Ação**, abaixo do nome da máquina virtual, clique em **Configurações**.

4.  No painel de navegação, clique em **processador**.

5.  Na página **processador** , defina o número de processadores como **1** ou **2** e clique em **OK**.



