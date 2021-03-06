---
description: 'Saiba mais sobre: Apêndice de administração simplificada'
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: Apêndice de administração simplificada
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 21b379b8138e95b70ebae91b34b8955e20715b3b
ms.sourcegitcommit: 6fbe337587050300e90340f9aa3e899ff5ce1028
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97599689"
---
# <a name="simplified-administration-appendix"></a>Apêndice de administração simplificada

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

-   [Caixa de diálogo Gerenciador do Servidor adicionar servidores (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)

-   [Status do servidor Gerenciador do Servidor remoto](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)

-   [Carregamento de módulo do Windows PowerShell](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)

-   [Hotfixes de emissão de RID para sistemas operacionais anteriores](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)

-   [Ntdsutil.exe instalar a partir de alterações de mídia](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)

## <a name="server-manager-add-servers-dialog-active-directory"></a><a name="BKMK_AddServers"></a>Caixa de diálogo Gerenciador do Servidor adicionar servidores (Active Directory)

A caixa de diálogo **adicionar servidores** permite pesquisar Active Directory de servidores, por sistema operacional, usando curingas e por local. A caixa de diálogo também permite o uso de consultas DNS por nome de domínio totalmente qualificado ou nome de prefixo. Essas pesquisas usam protocolos DNS e LDAP nativos implementados por meio do .NET, não o AD do Windows PowerShell no gateway de gerenciamento do AD por meio do SOAP, o que significa que os controladores de domínio contatados pelo Gerenciador do Servidor podem até mesmo executar o Windows Server 2003. Você também pode importar um arquivo com nomes de servidor para fins de provisionamento.

A pesquisa Active Directory usa os seguintes filtros LDAP:

```
(&(ObjectCategory=computer)

(&(ObjectCategory=computer)(cn=dc*)(OperatingSystemVersion=6.2*))

(&(ObjectCategory=computer)(OperatingSystemVersion=6.1*))

(&(ObjectCategory=computer)(OperatingSystemVersion=6.0*))

(&(ObjectCategory=computer)(|(OperatingSystemVersion=5.2*)(OperatingSystemVersion=5.1*)))

```

A pesquisa Active Directory retorna os seguintes atributos:

```
( dnsHostName )( operatingSystem )( cn )

```

## <a name="server-manager-remote-server-status"></a><a name="BKMK_ServerMgrStatus"></a>Status do servidor Gerenciador do Servidor remoto
Gerenciador do Servidor testa a acessibilidade de servidor remoto usando o protocolo de roteamento de endereços. Os servidores que não respondem às solicitações ARP não são listados, mesmo que estejam no pool.

Se o ARP responder, as conexões DCOM e WMI serão feitas ao servidor para retornar informações de status. Se RPC, DCOM e WMI estiverem inacessíveis, o Gerenciador do servidor não poderá gerenciar totalmente o servidor.

## <a name="windows-powershell-module-loading"></a><a name="BKMK_PSLoadModule"></a>Carregamento de módulo do Windows PowerShell
O Windows PowerShell 3,0 implementa o carregamento de módulos dinâmicos. O uso do cmdlet **Import-Module** normalmente não é mais necessário; em vez disso, simplesmente invocar o cmdlet, o alias ou a função carrega o módulo automaticamente.

Para ver os módulos carregados, use o cmdlet **Get-Module** .

```
Get-Module

```

![Administração simplificada](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)

Para ver todos os módulos instalados com suas funções e cmdlets exportados, use:

```
Get-Module -ListAvailable

```

O caso principal para usar o comando **Import-Module** é quando você precisa acessar o "ad:" unidade virtual do Windows PowerShell e nada mais já carregou o módulo. Por exemplo, usando os seguintes comandos:

```
import-module activedirectory
cd ad:
dir

```

## <a name="rid-issuance-hotfixes-for-previous-operating-systems"></a><a name="BKMK_Rid"></a>Hotfixes de emissão de RID para sistemas operacionais anteriores
Veja [uma atualização disponível para detectar e evitar muito consumo do pool de RID global em um controlador de domínio que esteja executando o Windows Server 2008 R2](https://support.microsoft.com/kb/2618669).

## <a name="ntdsutilexe-install-from-media-changes"></a><a name="BKMK_IFM"></a>Ntdsutil.exe instalar a partir de alterações de mídia
O Windows Server 2012 adiciona duas opções adicionais à ferramenta de linha de comando Ntdsutil.exe para o menu **IFM (criação de mídia IFM)** . Eles permitem que você crie lojas IFM sem primeiro executar uma desfragmentação offline do NTDS exportado. Arquivo de banco de dados DIT. Quando o espaço em disco não é um Premium, isso poupa tempo na criação da IFM.

A tabela a seguir descreve os dois novos itens de menu:

|Item de menu|Explicação|
|--|--|
|Criar NoDefrag% s completo|Criar mídia IFM sem desfragmentação para um DC completo do AD ou uma instância do AD/LDS na pasta% s|
|Criar NoDefrag completo do SYSVOL% s|Criar mídia IFM com SYSVOL e sem desfragmentação para um DC do AD completo na pasta% s|

![Captura de tela de uma janela de terminal que mostra o processo de criação de mídia IFM.](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)

![Captura de tela de uma janela de terminal que mostra a mídia IFM foi criada com êxito.](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)
