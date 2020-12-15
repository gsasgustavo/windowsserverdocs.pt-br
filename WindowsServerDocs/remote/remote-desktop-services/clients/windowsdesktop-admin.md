---
title: Cliente de Área de Trabalho do Windows para administradores
description: Informações sobre o cliente da Área de Trabalho do Windows úteis principalmente para administradores.
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 12/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: b4085868c136f2f8653f623e5a167a283f463eee
ms.sourcegitcommit: 7c0794e257f602bd71af5eb9a11b8a03d2b9adfd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97390314"
---
# <a name="windows-desktop-client-for-admins"></a>Cliente de Área de Trabalho do Windows para administradores

>Aplica-se a: Windows 10 e Windows 7

Este tópico tem informações adicionais sobre o cliente da Área de Trabalho do Windows que os administradores acharão úteis. Para obter informações de uso básicas, confira [Introdução ao cliente da Área de Trabalho do Windows](windowsdesktop.md).

## <a name="installation-options"></a>Opções de instalação

Embora os usuários possam instalar o cliente diretamente depois de baixá-lo, se você estiver implantando em vários dispositivos, talvez também queira implantar o cliente neles por outros meios. A implantação usando políticas de grupo ou o Microsoft Endpoint Configuration Manager permite que você execute o instalador silenciosamente usando uma linha de comando. Execute os seguintes comandos para implantar o cliente por dispositivo ou por usuário.

### <a name="per-device-installation"></a>Instalação por dispositivo

```
msiexec.exe /I <path to the MSI> /qn ALLUSERS=1
```

### <a name="per-user-installation"></a>Instalação por usuário

```
msiexec.exe /i `<path to the MSI>` /qn ALLUSERS=2 MSIINSTALLPERUSER=1
```

## <a name="configuration-options"></a>Opções de configuração

Esta seção descreve as novas opções de configuração para esse cliente.

### <a name="configure-update-notifications"></a>Configurar notificações de atualização

Por padrão, o cliente notifica você sempre que há uma atualização e se atualiza automaticamente quando o cliente é fechado e não tem nenhuma conexão ativa. Mesmo sem conexões ativas, o processo msrdc.exe é executado em segundo plano para permitir que você se reconecte rapidamente quando reabrir o cliente. Você pode parar o msrdc.exe clicando com o botão direito do mouse no ícone da Área de Trabalho Virtual do Windows na área da bandeja do sistema e selecionando **Desconectar todas as sessões** no menu suspenso.

Para desativar as notificações, defina as seguintes informações do Registro:

- **Chave:** HKLM\Software\Microsoft\MSRDC\Policies
- **Tipo:** REG_DWORD
- **Nome:** AutomaticUpdates
- **Dados:** 0 = Desabilitar notificações e desligar a atualização automática. 1 = Mostrar notificações e desligar a atualização automática. 2 = mostrar notificações e atualizar automaticamente no fechamento.

### <a name="configure-user-groups"></a>Configurar grupos de usuário

É possível configurar o cliente para um dos seguintes tipos de grupos de usuário, que determina quando o cliente recebe atualizações.

#### <a name="insider-group"></a>Grupo de Participantes do Programa Windows Insider

O grupo de Participantes do Programa Windows Insider destina-se a validação antecipada e é composto por administradores e seus usuários selecionados. O grupo de Participantes do Programa Windows Insider funciona como uma execução de teste para detectar problemas na atualização que possam afetar o desempenho antes de serem liberados para o grupo público.

> [!NOTE]
> Recomendamos que cada organização tenha alguns usuários no grupo de Participantes do Programa Windows Insider para testar atualizações e detectar problemas no início.

No grupo de Participantes do Programa Windows Insider, uma nova versão do cliente é liberada para os usuários na segunda terça-feira de cada mês para validação antecipada. Se a atualização não tiver problemas, ela será liberada para o grupo público duas semanas depois. Os usuários no grupo de Participantes do Programa Windows Insider receberão notificações de atualização automaticamente sempre que as atualizações estiverem prontas. É possível encontrar informações mais detalhadas sobre alterações no cliente em [Novidades do cliente da Área de Trabalho do Windows](windowsdesktop-whatsnew.md).

Para configurar o cliente para o grupo de Participantes do Programa Windows Insider, defina as seguintes informações do Registro:

- **Chave:** HKLM\Software\Microsoft\MSRDC\Policies
- **Tipo:** REG_SZ
- **Nome:** ReleaseRing
- **Dados:** participantes do Programa Windows Insider

#### <a name="public-group"></a>Grupo público

Este grupo é para todos os usuários e é a versão mais estável. Não é necessário configurar mais nada para esse grupo.

O grupo Público recebe a versão do cliente que foi testada pelo grupo de participantes do Programa Windows Insider a cada quarta terça-feira de cada mês. Todos os usuários no grupo Público receberão uma notificação de atualização se essa configuração estiver habilitada.
