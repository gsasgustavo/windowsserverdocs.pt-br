---
title: Configurar máquinas virtuais que executam o Windows 7 sem mais de 4 processadores virtuais
description: Saiba o que fazer quando uma máquina virtual que executa o Windows 7 estiver configurada com mais de 4 processadores virtuais.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 8fcf0868-b543-4f94-aee7-35324346da55
ms.date: 8/16/2016
ms.openlocfilehash: f52884ea6ce7298980f42b1aca876866c7dbaa77
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846402"
---
# <a name="configure-virtual-machines-running-windows-7-with-no-more-than-4-virtual-processors"></a>Configurar máquinas virtuais que executam o Windows 7 sem mais de 4 processadores virtuais

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Erro|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>**Problema**
*Uma máquina virtual que executa o Windows 7 está configurada com mais de 4 processadores virtuais.*

## <a name="impact"></a>**Impacto**
*A Microsoft não oferece suporte à configuração das seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>**Resolução**
*Desligue a máquina virtual e remova um ou mais processadores virtuais.*

#### <a name="to-remove-virtual-processors"></a>Para remover processadores virtuais

1.  Abra o Gerenciador do Hyper-V. Clique em **Iniciar**, vá em **Ferramentas Administrativas** e clique em **Gerenciador do Hyper-V**.

2.  No painel de resultados, em **máquinas virtuais**, selecione a máquina virtual que você deseja configurar. O estado da máquina virtual deve ser listado como **desativado**. Se não estiver, clique com o botão direito do mouse na máquina virtual e clique em **desligar**.

3.  No painel **Ação**, abaixo do nome da máquina virtual, clique em **Configurações**.

4.  No painel de navegação, clique em **processador**.

5.  Na página **processador** , defina o número de processadores para **3** ou menos e clique em **OK**.



