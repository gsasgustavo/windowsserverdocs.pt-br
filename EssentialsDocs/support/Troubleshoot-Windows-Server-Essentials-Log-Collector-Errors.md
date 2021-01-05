---
title: Solucionar problemas de erros de coletores de log do Windows Server Essentials
description: Saiba como solucionar problemas encontrados ao executar o coletor de logs.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: fa2e1685-31c0-4d4f-a10a-6c8885dfc493
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 0da27272f3daf5159e5f6ac868788382b1bf11a7
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810216"
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Solucionar problemas de erros de coletores de log do Windows Server Essentials

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Quando executar o coletor de Log, você pode encontrar um dos seguintes erros. Para resolver um problema, siga as orientações fornecidas para o erro associado.

> [!NOTE]
> Neste documento, os computadores em sua rede, além do servidor, são chamados de computadores de rede.

###  <a name="the-destination-folder-is-not-valid"></a><a name="BKMK_TheDestinationFolderIsNotValid"></a> A pasta de destino não é válida
 **Causa:** a pasta na qual você está tentando copiar os arquivos de log pode não existir ou pode não ter espaço suficiente para conter os arquivos.

 **Solution:** verifique se a pasta selecionada existe e se há espaço livre suficiente na unidade de arquivos. Você também deve garantir que há espaço livre suficiente restante na pasta temporária na unidade.

###  <a name="a-network-error-has-occurred"></a><a name="BKMK_ANetworkErrorHasOccurred"></a> Ocorreu um erro de rede
 **Causa:** pode haver um problema de rede no computador da rede ou no servidor.

 **Solução:** certifique-se de que todos os computadores e dispositivos de rede estejam ligados e conectados à rede. Se não for possível resolver o problema, entre em contato com a pessoa que mantém a sua rede para obter assistência.

###  <a name="cannot-collect-log-files-for-the-computer"></a><a name="BKMK_CannotCollectLogFiles"></a> Não é possível coletar arquivos de log para o computador
 **Cause:** o coletor de log não pode ser instalado no computador porque o computador não se pode se conectar com êxito ao servidor usando o assistente Conectar Computador ao Servidor.

 **Solução:** Para obter informações sobre como resolver problemas relacionados a conexões com o servidor, consulte [solucionar problemas de conexão de computadores com o servidor](https://go.microsoft.com/fwlink/p/?LinkID=241492).

 Se você ainda não conseguir conectar o computador ao servidor, você pode copiar os arquivos de log manualmente para uma unidade flash USB da seguinte maneira:

-   Para computadores cliente que executam o Windows 7, Windows 8 ou Windows MultiPoint Server, você pode copiar a pasta **Logs** localizada em **%sysdir%\programdata\Microsoft\Windows Server**.

###  <a name="you-do-not-have-permission-to-save-the-log-files-to-the-selected-folder"></a><a name="BKMK_YouDoNotHavePermission"></a> Você não tem permissão para salvar os arquivos de log na pasta selecionada
 **Cause:** você pode não ter permissão de gravação para a pasta selecionada para salvar os arquivos de log.

 **Solução:** Se você estiver usando o caminho padrão para salvar arquivos de log, verifique se você tem permissão de gravação para a pasta compartilhada **\\ \\<ServerName \> \Logs**. Se estiver armazenando logs em um computador da rede, certifique-se de que você tenha permissão de gravação para a pasta que selecionada para salvar os arquivos de log.

###  <a name="the-computer-is-not-configured-properly-to-collect-the-log-files"></a><a name="BKMK_TheComputerIsNotConfiguredProperly"></a> O computador não está configurado corretamente para coletar os arquivos de log
 **Causa:** o computador não foi configurado corretamente para o coletor de log.

 **Solução:** reinstalar o coletor de log. Consulte [Reinstalar o coletor de log](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall).

###  <a name="an-unknown-error-occurred"></a><a name="BKMK_AnUnknownErrorOccurred"></a> Ocorreu um erro desconhecido
 **Causa:** desconhecida.

 **Solução 1:** reinstalar o coletor de log. Se o erro ocorrer novamente, verifique se não há problemas de conectividade. Você também pode tentar reinstalar o coletor de log. Consulte [Reinstalar o coletor de log](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall). Se não for possível resolver o problema, entre em contato com a pessoa que mantém a sua rede para obter assistência.

 **Solução 2:** primeiro, tente abrir a pasta na qual os arquivos de log estão salvos. Se o arquivo zip com o nome de computador já tiver sido gerado, ignore este erro e use os arquivos de log. Se não houver nenhum arquivo de log gerado, execute novamente o coletor de log. Se o erro ocorrer novamente, verifique se não há problemas de conectividade. Você também pode tentar reinstalar o coletor de log. Consulte [Reinstalar o coletor de log](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall). Se não for possível resolver o problema, entre em contato com a pessoa que mantém a sua rede para obter assistência.