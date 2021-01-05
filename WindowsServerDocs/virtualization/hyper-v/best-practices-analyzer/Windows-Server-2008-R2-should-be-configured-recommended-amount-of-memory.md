---
title: O Windows Server 2008 R2 deve ser configurado com a quantidade recomendada de memória
description: Saiba o que fazer quando uma máquina virtual que executa o Windows Server 2008 R2 é configurada com menos do que a quantidade recomendada de RAM, que é de 2 GB.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 26872519-ccf0-4757-827f-8df2a7a2b9f9
ms.date: 8/16/2016
ms.openlocfilehash: 183f09c40a3d62afc46cc72e12de20adb2b231a4
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834211"
---
# <a name="windows-server-2008-r2-should-be-configured-with-the-recommended-amount-of-memory"></a>O Windows Server 2008 R2 deve ser configurado com a quantidade recomendada de memória

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

*Uma máquina virtual que executa o Windows Server 2008 R2 é configurada com menos do que a quantidade recomendada de RAM, que é de 2 GB.*

## <a name="impact"></a>Impacto

*O sistema operacional convidado e os aplicativos podem não ter um bom desempenho. Pode não haver memória suficiente para executar vários aplicativos ao mesmo tempo. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machine names>

## <a name="resolution"></a>Resolução

*Use o Gerenciador do Hyper-V para aumentar a memória alocada para esta máquina virtual para pelo menos 2 GB.*

### <a name="to-increase-the-memory-using-hyper-v-manager"></a>Para aumentar a memória usando o Gerenciador do Hyper-V

1.  Abra o Gerenciador do Hyper-V. Clique em **Iniciar**, vá em **Ferramentas Administrativas** e clique em **Gerenciador do Hyper-V**.

2.  No painel de resultados, em **máquinas virtuais**, selecione a máquina virtual que você deseja configurar. O estado da máquina virtual deve ser listado como **desativado**. Se não estiver, clique com o botão direito do mouse na máquina virtual e clique em **desligar**.

3.  No painel **Ação**, abaixo do nome da máquina virtual, clique em **Configurações**.

4.  No painel de navegação, clique em **memória**.

5.  Na página **memória** , defina a **RAM de inicialização** para pelo menos 2 GB e clique em **OK**.

### <a name="increase-the-memory-using-windows-powershell"></a>Aumentar a memória usando o Windows PowerShell

1.  Abra o Windows PowerShell. (Na área de trabalho, clique em **Iniciar** e comece a digitar **Windows PowerShell**.)

2.  Clique com o botão direito do mouse em **Windows PowerShell** e clique em **Executar como administrador**.

3.  Execute este comando depois de substituir \<MyVM> pelo nome da sua máquina virtual:

```
Set-VMMemory <MyVM> -StartupBytes 2GB
```

## <a name="see-also"></a>Consulte Também
[Set-VMMemory](/powershell/module/hyper-v/set-vmmemory)
