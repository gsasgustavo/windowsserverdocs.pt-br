---
title: O Windows Vista deve ser configurado com a quantidade recomendada de memória
description: Fornece instruções para resolver o problema relatado por essa regra de Analisador de Práticas Recomendadas.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 64f4e53b-4adb-4e1d-bc48-c24f5f9d222f
ms.date: 8/16/2016
ms.openlocfilehash: ca492081383b962f85e8c28bc9e240a9ed62acfe
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96866375"
---
# <a name="windows-vista-should-be-configured-with-the-recommended-amount-of-memory"></a>O Windows Vista deve ser configurado com a quantidade recomendada de memória

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

*Uma máquina virtual que executa o Windows Vista é configurada com menos do que a quantidade recomendada de RAM, que é de 1 GB.*

## <a name="impact"></a>Impacto

*O sistema operacional convidado e os aplicativos podem não ter um bom desempenho. Pode não haver memória suficiente para executar vários aplicativos ao mesmo tempo. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machine names>

## <a name="resolution"></a>Resolução

*Use o Gerenciador do Hyper-V para aumentar a memória alocada para esta máquina virtual para pelo menos 1 GB.*

### <a name="to-increase-the-memory-allocated-to-a-virtual-machine"></a>Para aumentar a memória alocada para uma máquina virtual

1.  Abra o Gerenciador do Hyper-V. Clique em **Iniciar**, vá em **Ferramentas Administrativas** e clique em **Gerenciador do Hyper-V**.

2.  No painel de resultados, em **máquinas virtuais**, selecione a máquina virtual que você deseja configurar. O estado da máquina virtual deve ser listado como **desativado**. Se não estiver, clique com o botão direito do mouse na máquina virtual e clique em **desligar**.

3.  No painel **Ação**, abaixo do nome da máquina virtual, clique em **Configurações**.

4.  No painel de navegação, clique em **memória**.

5.  Na página **memória** , defina a **RAM de inicialização** para pelo menos 1 GB e clique em **OK**.

### <a name="increase-the-memory-using-windows-powershell"></a>Aumentar a memória usando o Windows PowerShell

1.  Abra o Windows PowerShell. (Na área de trabalho, clique em **Iniciar** e comece a digitar **Windows PowerShell**.)

2.  Clique com o botão direito do mouse em **Windows PowerShell** e clique em **Executar como administrador**.

3.  Execute este comando depois de substituir \<MyVM> pelo nome da sua máquina virtual:

```
Set-VMMemory <MyVM> -StartupBytes 1GB
```

## <a name="see-also"></a>Consulte Também
[Set-VMMemory](/powershell/module/hyper-v/set-vmmemory)
