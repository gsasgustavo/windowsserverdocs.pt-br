---
title: Uma máquina virtual que executa o Windows Server 2008 e configurada com Memória Dinâmica deve usar os valores recomendados para as configurações de memória
description: Saiba como usar o Gerenciador do Hyper-V ou o Windows PowerShell para aumentar a memória mínima para pelo menos 256 MB e a memória de inicialização e máxima para pelo menos 512 MB.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: f4c05a2c-52d0-4fa2-987d-37a6ed667134
ms.date: 8/16/2016
ms.openlocfilehash: 2f7ffa9b73c69b114d90090c7de88fe03f00e0fc
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834091"
---
# <a name="a-virtual-machine-running-windows-server-2008-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Uma máquina virtual que executa o Windows Server 2008 e configurada com Memória Dinâmica deve usar os valores recomendados para as configurações de memória

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*Uma ou mais máquinas virtuais estão configuradas para usar Memória Dinâmica com menos que a quantidade de memória recomendada para o Windows Server 2008.*

## <a name="impact"></a>Impacto
*O sistema operacional convidado nas seguintes máquinas virtuais pode não ser executado ou pode ser executado de forma não confiável:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Use o Gerenciador do Hyper-V ou o Windows PowerShell para aumentar a memória mínima para pelo menos 256 MB e a memória de inicialização e máxima para pelo menos 512 MB.*

#### <a name="increase-memory-using-hyper-v-manager"></a>Aumentar a memória usando o Gerenciador do Hyper-V

1.  Abra o Gerenciador do Hyper-V. (Em Gerenciador do Servidor, clique em **ferramentas**  >  **Gerenciador do Hyper-V**.)

2.  Na lista de máquinas virtuais, clique com o botão direito do mouse no que você deseja e clique em **configurações**.

3.  No painel de navegação, clique em **memória**.

4.  Altere a **RAM** para pelo menos 512 MB.

5.  Em **memória dinâmica**, altere o **mínimo de RAM** para pelo menos 256 MB e o **máximo de RAM** para pelo menos 512 MB.

6.  Clique em **OK**.

### <a name="increase-memory-using-windows-powershell"></a>Aumentar a memória usando o Windows PowerShell

1.  Abra o Windows PowerShell. (Na área de trabalho, clique em **Iniciar** e comece a digitar **Windows PowerShell**.)

2.  Clique com o botão direito do mouse em **Windows PowerShell** e clique em **Executar como administrador**.

3.  Execute um comando semelhante ao seguinte, substituindo MyVM pelo nome da sua máquina virtual e os valores de memória com pelo menos os valores mostrados abaixo.

```
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB
```



