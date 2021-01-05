---
title: O número de máquinas virtuais em execução ou configuradas deve estar dentro dos limites com suporte
description: Saiba o que fazer quando mais máquinas virtuais estiverem em execução ou configuradas do que têm suporte.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 9d3c4aa3-8416-46ec-a253-26dc98088d7b
ms.date: 8/16/2016
ms.openlocfilehash: 257c929364614dd058721012ff80ea352479b5d5
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834821"
---
# <a name="the-number-of-running-or-configured-virtual-machines-must-be-within-supported-limits"></a>O número de máquinas virtuais em execução ou configuradas deve estar dentro dos limites com suporte

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Erro
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*Mais máquinas virtuais estão em execução ou configuradas do que há suporte.*

## <a name="impact"></a>Impacto
*A Microsoft não oferece suporte ao número atual de máquinas virtuais em execução ou configuradas neste servidor.*

## <a name="resolution"></a>Resolução
*Mova uma ou mais máquinas virtuais para outro servidor.*

Para obter detalhes sobre as configurações máximas com suporte para o Hyper-V, como o número de máquinas virtuais em execução, consulte [planejar a escalabilidade do Hyper-v no Windows Server 2016](../plan/plan-hyper-v-scalability-in-windows-server.md).

Para mover uma máquina virtual para outro servidor, você pode:

- Exporte a máquina virtual do servidor atual e importe-a para um novo servidor, conforme descrito abaixo.
- Faça uma migração ao vivo:
    - Se esse servidor pertencer a um cluster de failover, use as ferramentas fornecidas com o recurso de clustering de failover. Para obter instruções, consulte [migração ao vivo, migração rápida ou mover uma máquina virtual do nó para o nó](https://go.microsoft.com/fwlink/?LinkID=181519).
    - Se este for um servidor autônomo, consulte as instruções em [configurar migração ao vivo e migrar máquinas virtuais sem clustering de failover](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134199(v=ws.11))

### <a name="to-export-a-virtual-machine"></a>Para exportar uma máquina virtual

   > [!IMPORTANT]
   > Se o host Hyper-V que você está exportando pertencer a um domínio e você quiser armazenar os arquivos exportados em um local remoto, o host Hyper-V deverá ser configurado para delegação restrita. Um local remoto pode ser uma pasta de rede compartilhada ou uma pasta no host para o qual você está importando. A delegação restrita permite que a conta de computador do host Hyper-V forneça credenciais delegadas para o serviço CIFS (sistema de arquivos da Internet comum) para o computador remoto. Para obter instruções sobre como configurar a delegação restrita, consulte a seção seguindo as instruções de exportação e importação, abaixo.

1.  Abra o Gerenciador do Hyper-V. Clique em **Iniciar**, vá em **Ferramentas Administrativas** e clique em **Gerenciador do Hyper-V**.

2.  No painel de resultados, em **máquinas virtuais**, clique com o botão direito do mouse em uma máquina virtual e clique em **Exportar**.

3.  Na caixa de diálogo **exportar uma máquina virtual** , digite ou navegue até um local que tenha espaço livre suficiente para armazenar todos os recursos da máquina virtual. Quando você exporta uma máquina virtual, todos os discos rígidos virtuais (arquivos. VHD ou. vhdx), pontos de verificação (arquivos. avhd) e arquivos de estado salvo associados à máquina virtual são copiados para a pasta especificada.

4.  Clique em **Exportar**.

Depois de exportar as máquinas virtuais, importe as máquinas virtuais para o outro servidor.

### <a name="to-import-a-virtual-machine-to-another-server"></a>Para importar uma máquina virtual para outro servidor

1.  Conecte-se ao servidor que executa o Hyper-V e abra o Gerenciador do Hyper-V.

2.  No painel **ação** , clique em **importar máquina virtual**.

3.  Na caixa de diálogo **importar máquina virtual** , especifique o local onde você exportou a máquina virtual. A menos que você queira reimportar essa máquina virtual, deixe as configurações de importação como estão.

4.  Clique em **Importar**.

### <a name="to-configure-constrained-delegation"></a>Para configurar a delegação restrita

A associação no grupo **Administradores de domínio** é necessária para concluir este procedimento.

1.  Em um computador com o recurso ferramentas de Active Directory Domain Services instalado, em **Ferramentas administrativas**, abra **Active Directory usuários e computadores** e, em seguida, navegue até a conta de computador do computador que executa o Hyper-V.

    > [!NOTE]
    > Se **Active Directory usuários e computadores** não estiver listado, instale o recurso de ferramentas de Active Directory Domain Services. Para obter instruções, consulte [installing ferramentas de administração de servidor remoto for AD DS](https://go.microsoft.com/fwlink/?LinkId=140463) ( https://go.microsoft.com/fwlink/?LinkId=140463) .

2.  Clique com o botão direito do mouse na conta do computador que executa o Hyper-V e clique em **Propriedades**.

3.  Na guia **delegação** , clique em **selecionar este computador para delegação apenas para serviços especificados** e, em seguida, clique em **usar qualquer protocolo de autenticação**.

4.  Para permitir que a conta de computador do Hyper-V apresente credenciais delegadas ao computador remoto:

    1.  Clique em **Adicionar**.

    2.  Na caixa de diálogo **Adicionar serviços** , clique em **usuários ou computadores**, selecione o computador remoto e clique em **OK**.

    3.  Na lista **serviços disponíveis** , selecione o protocolo **CIFS** (também conhecido como protocolo SMB) e, em seguida, clique em **Adicionar**.