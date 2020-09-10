---
title: Configuração do Sc.exe
description: Saiba como alterar as configurações de serviço usando o utilitário sc.exe
ms.topic: reference
ms.assetid: ad4d68a6-efe5-452b-8501-7f1f1c552a4a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 06/05/2018
ms.openlocfilehash: 55432910455896434a1857d17016519bedb51caf
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637131"
---
# <a name="scexe-config"></a>Configuração do Sc.exe

Modifica o valor das entradas de um serviço no registro e no banco de dados do Gerenciador de controle de serviço.

## <a name="syntax"></a>Sintaxe

```
sc.exe [<ServerName>] config [<ServiceName>] [type= {own | share | kernel | filesys | rec | adapt | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto}] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------|-----------|
|\<ServerName>|Especifica o nome do servidor remoto no qual o serviço está localizado. O nome deve usar o formato UNC (Convenção de nomenclatura universal) (por exemplo, \\ \\ meuservidor). Para executar SC.exe localmente, omita esse parâmetro.|
|\<ServiceName>|Especifica o nome do serviço retornado pela operação **GetKeyName** .|
|Type = {próprio \| compartilhamento de \| arquivos de kernel \| os REC. interagir com o \| \| \| tipo = {próprio \| compartilhamento}} | Especifica o tipo de serviço.</br>**próprio** -especifica um serviço que é executado em seu próprio processo. Ele não compartilha um arquivo executável com outros serviços. Esse é o valor padrão.</br>**compartilhamento** – especifica um serviço que é executado como um processo compartilhado. Ele compartilha um arquivo executável com outros serviços.</br>**kernel** -especifica um driver.</br>**arquivos** -especifica um driver de sistema de arquivos.</br>**REC** -especifica um driver reconhecido pelo sistema de arquivos que identifica os sistemas de arquivos usados no computador.</br>**adaptação** – especifica um driver de adaptador que identifica dispositivos de hardware, como teclados, mouses e unidades de disco.</br>**interagir** -especifica um serviço que pode interagir com a área de trabalho, recebendo entrada de usuários. Os serviços interativos devem ser executados na conta LocalSystem. Esse tipo deve ser usado em conjunto com **Type = próprio** ou **Type = Shared** (por exemplo, **Type = interaja** **Type =** is). Usar **Type = interagir** por si só gerará um erro.|
|início = {a \| demanda automática do sistema de inicialização foi \| \| \| desabilitada \| com atraso-automática}|Especifica o tipo de início para o serviço.</br>**boot** -especifica um driver de dispositivo que é carregado pelo carregador de inicialização.</br>**sistema** -especifica um driver de dispositivo que é iniciado durante a inicialização do kernel.</br>**automaticamente** especifica um serviço que é iniciado automaticamente cada vez que o computador é reiniciado e é executado mesmo que ninguém faça logon no computador.</br>**demanda** -especifica um serviço que deve ser iniciado manualmente. Esse será o valor padrão se **Start =** não for especificado.</br>**Disabled** -especifica um serviço que não pode ser iniciado. Para iniciar um serviço desabilitado, altere o tipo de início para algum outro valor.</br>**atrasada –** especifica automaticamente um serviço que inicia de forma automática um curto período após a inicialização de outros serviços automáticos.|
|erro = { \| \| ignorar crítico normal grave \| }|Especifica a severidade do erro se o serviço não for iniciado no momento da inicialização.</br>**normal** – especifica que o erro é registrado e uma caixa de mensagem é exibida, informando ao usuário que um serviço falhou ao iniciar. A inicialização continuará. Essa é a configuração padrão.</br>**grave** -especifica que o erro é registrado (se possível). O computador tenta reiniciar com a última configuração válida conhecida. Isso pode fazer com que o computador possa ser reiniciado, mas o serviço ainda pode não ser executado.</br>**crítico** -especifica que o erro é registrado (se possível). O computador tenta reiniciar com a última configuração válida conhecida. Se a configuração válida mais conhecida falhar, a inicialização também falhará e o processo de inicialização é interrompido com um erro de parada.</br>**ignorar** – especifica que o erro é registrado e a inicialização continua. Nenhuma notificação é dada ao usuário além de registrar o erro no log de eventos.|
|BinPath = \<BinaryPathName>|Especifica um caminho para o arquivo binário do serviço.|
|Grupo = \<LoadOrderGroup>|Especifica o nome do grupo do qual esse serviço é membro. A lista de grupos é armazenada no registro, na subchave **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** . O valor padrão é nulo.|
|marca = {sim \| não}|Especifica se deve ou não obter um TagID da chamada CreateService. As marcas são usadas somente para os drivers inicialização e início do sistema.|
|depend = \<dependencies>|Especifica os nomes de serviços ou grupos que devem iniciar antes desse serviço. Os nomes são separados por barras (/).|
|obj = { \<AccountName> \| \<ObjectName> }|Especifica um nome de uma conta na qual um serviço será executado ou especifica um nome do objeto de driver do Windows no qual o driver será executado. A configuração padrão é **LocalSystem**.|
|DisplayName = \<DisplayName>|Especifica um nome descritivo para identificar o serviço em programas de interface do usuário. Por exemplo, o nome da subchave de um serviço específico é **wuauserv**, que tem um nome de exibição mais amigável de atualizações automáticas.|
|senha = \<Password>|Especifica uma senha. Isso será necessário se uma conta diferente da conta LocalSystem for usada.|
|/?|Exibe a ajuda no prompt de comando.|

## <a name="remarks"></a>Comentários

-   Para cada opção de linha de comando (parâmetro), o sinal de igual faz parte do nome da opção.
-   Um espaço é necessário entre uma opção e seu valor (por exemplo, **tipo = próprio**. Se o espaço for omitido, a operação falhará.

## <a name="examples"></a>Exemplos

Para especificar um caminho binário para o serviço NEWSERVICE, digite:
```
sc.exe config NewService binpath= ntsd -d c:\windows\system32\NewServ.exe
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
