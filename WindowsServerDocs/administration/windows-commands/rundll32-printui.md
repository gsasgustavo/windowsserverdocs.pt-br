---
title: rundll32 printui.dll, PrintUIEntry
description: Artigo de referência para o comando rundll32 printui.dll, PrintUIEntry, que automatiza muitas tarefas de configuração de impressora.
ms.topic: reference
ms.assetid: 12fb48b6-5dd8-4cc0-8808-e6a681aceb84
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 05/25/2018
ms.openlocfilehash: 8ad0b9b3cfdca8d9ed82cc980d29df7c885bac46
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388447"
---
# <a name="rundll32-printuidllprintuientry"></a>rundll32 printui.dll, PrintUIEntry

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Automatiza muitas tarefas de configuração de impressora. printui.dll é o arquivo executável que contém as funções usadas pelas caixas de diálogo de configuração de impressora. Essas funções também podem ser chamadas de dentro de um script ou de um arquivo em lotes de linha de comando, ou podem ser executadas interativamente no prompt de comando.

## <a name="syntax"></a>Sintaxe

```
rundll32 printui.dll PrintUIEntry [baseparameter] [modificationparameter1] [modificationparameter2] [modificationparameterN]
```

Você também pode usar as seguintes sintaxes alternativas, embora os exemplos neste tópico usem a sintaxe anterior:

```
rundll32 printui.dll,PrintUIEntry [baseparameter] [modificationparameter1] [modificationparameter2] [ModificationParameterN]
```

```
rundll32 printui PrintUIEntry [baseparameter] [modificationparameter1] [modificationparameter2] [modificationparameterN]
```

```
rundll32 printui,PrintUIEntry [baseparameter] [modificationparameter1] [modificationparameter2] [modificationparameterN]
```

### <a name="parameters"></a>Parâmetros

Há dois tipos de parâmetros: parâmetros de base e parâmetros de modificação. Parâmetros de base especifique a função que o comando deve executar. Somente um desses parâmetros pode aparecer em uma determinada linha de comando. Em seguida, você pode modificar o parâmetro base usando um ou mais dos parâmetros de modificação se eles forem aplicáveis ao parâmetro base (nem todos os parâmetros de modificação têm suporte de todos os parâmetros de base).

| Parâmetros de base | Descrição |
|--|--|
| /dl | Exclui a impressora local. |
| /dn | Exclui uma conexão de impressora de rede. |
| /DD | Exclui um driver de impressora. |
| /e | Exibe as preferências de impressão para uma determinada impressora. |
| /GA | Adiciona uma conexão de impressora por computador (a conexão está disponível para qualquer usuário nesse computador ao fazer logon). |
| /GE | Exibe conexões de impressora por computador em um computador. |
| /gd | Exclui uma conexão de impressora por computador (a conexão é excluída da próxima vez que um usuário fizer logon). |
| /ia | Instala um driver de impressora usando um arquivo. inf. |
| /id | Instala um driver de impressora usando o assistente para adicionar driver de impressora. |
| /If | Instala uma impressora usando um arquivo. inf. |
| /ii | Instala uma impressora usando o assistente para adicionar impressora com um arquivo. inf. |
| /il | Instala uma impressora usando o assistente para adicionar impressora. |
| /in | Conecta-se a uma impressora de rede remota. |
| /ip | Instala uma impressora usando o assistente de instalação de impressora de rede (disponível na interface do usuário do gerenciamento de impressão). |
| /k | imprime uma página de teste em uma impressora. |
| /o | Exibe a fila de uma impressora. |
| /p | Exibe as propriedades de uma impressora. Ao usar esse parâmetro, você também deve especificar um valor para o parâmetro de modificação **/n [name]**. |
| /s | Exibe as propriedades de um servidor de impressão. Se você quiser exibir o servidor de impressão local, não será necessário usar um parâmetro de modificação. No entanto, se você quiser exibir um servidor de impressão remoto, deverá especificar o parâmetro de modificação **/c [name]** . |
| /Ss | Especifica que tipo de informações de uma impressora serão armazenadas. Se nenhum dos valores de **/SS** for especificado, o comportamento padrão será como se todos fossem especificados. Use esse parâmetro base com os seguintes valores colocados no final da linha de comando:<ul><li>**2**: armazena as informações contidas na estrutura de printER_INFO_2 da impressora. Essa estrutura contém as informações básicas sobre a impressora, como nome, nome do servidor, nome da porta e nome do compartilhamento.</li><li>**7**: usado para armazenar as informações do serviço de diretório contidas na estrutura de printER_INFO_7.</li><li>**c**: armazena as informações de perfil de cor de uma impressora.</li><li>**d**: armazena dados específicos da impressora, como a ID de hardware da impressora.</li><li>**s**: armazena o descritor de segurança da impressora.</li><li>**g**: armazena as informações na estrutura DEVmode global dos s da impressora.</li><li>**m**: armazena as configurações mínimas para a impressora. Isso é equivalente a especificar **2** **d**e **g**.</li><li>**u**: armazena as informações na estrutura de DEVmode por usuário da impressora.</li></ul> |
| /Sr | Especifica quais informações sobre uma impressora são restauradas e como os conflitos nas configurações são manipulados. Use com os seguintes valores colocados no final da linha de comando:<ul><li>**2**: restaura as informações contidas na estrutura da impressora s printER_INFO_2. Essa estrutura contém as informações básicas sobre a impressora, como nome, nome do servidor, nome da porta e nome do compartilhamento.</li><li>**7**: restaura as informações do serviço de diretório contidas na estrutura de printER_INFO_7.</li><li>**c**: restaura as informações de perfil de cor de uma impressora.</li><li>**d**: restaura dados específicos da impressora, como a ID de hardware da impressora.</li><li>**s**: restaura o descritor de segurança da impressora.</li><li>**g**: restaura as informações na estrutura DEVmode global dos s da impressora.</li><li>**m**: restaura as configurações mínimas para a impressora. Isso é equivalente a especificar **2**, **d**e **g**.</li><li>**u** restaura as informações na estrutura de DEVmode s de impressão por usuário.</li><li>**r**: se o nome da impressora armazenada no arquivo for diferente do nome da impressora que está sendo restaurada, use o nome da impressora atual. Isso não pode ser especificado com **f**. Se nem **r** nem **f** forem especificados e os nomes não corresponderem, a restauração das configurações falhará.</li><li>**f**: se o nome da impressora armazenada no arquivo for diferente do nome da impressora que está sendo restaurada, use o nome da impressora no arquivo. Isso não pode ser especificado com o **r**. Se nem **f** nem **r** forem especificados e os nomes não corresponderem, a restauração das configurações falhará.</li><li>**p**: se o nome da porta no arquivo que está sendo restaurado não corresponder ao nome da porta atual da impressora que está sendo restaurada, o nome da porta atual da impressora será usado.</li><li>**h**: se a impressora que está sendo restaurada não puder ser compartilhada usando o nome do compartilhamento de recursos no arquivo de configurações salvas, tente compartilhar a impressora com o nome do compartilhamento atual ou com um novo nome de compartilhamento gerado se nem **h** nem **h** forem especificadas e a impressora que está sendo restaurada não puder ser compartilhada com o nome do compartilhamento salvo e a restauração falhar.</li><li>**h**: se a impressora que está sendo restaurada não puder ser compartilhada com o nome do compartilhamento salvo, não compartilhe a impressora. Se nem **h** nem **h** forem especificadas e a impressora que está sendo restaurada não puder ser compartilhada com o nome do compartilhamento salvo, a restauração falhará.</li><li>**i**: se o driver no arquivo de configurações salvo não corresponder ao driver da impressora que está sendo restaurada, a restauração falhará. |
| /Xg | Recupera as configurações de uma impressora. |
| /Xs | Define as configurações de uma impressora. |
| /y | Define a impressora que está sendo instalada como a impressora padrão. |
| /? | Exibe a ajuda no produto para o comando e seus parâmetros associados. |
| @ [arquivo] | Especifica um arquivo de argumento de linha de comando e insere diretamente o texto nesse arquivo na linha de comando. |

| Parâmetros de modificação | Descrição |
|--|--|
| /a [arquivo] | Especifica o nome do arquivo binário. |
| /b [nome] | Especifica o nome da impressora base. |
| /c [nome] | Especifica o nome do computador se a ação a ser executada estiver em um computador remoto. |
| /f [arquivo] | Especifica o caminho UNC (Convenção de nomenclatura universal) e o nome do nome do arquivo. inf ou o nome do arquivo de saída, dependendo da tarefa que você está executando. Use **/f [File]** para especificar um arquivo. inf dependente. |
| /F [arquivo] | Especifica o caminho UNC e o nome de um arquivo. inf que o arquivo. inf especificado com **/f [File]** depende. |
| /h [arquitetura] | Especifica a arquitetura do driver. Use um dos seguintes: **x86**, **x64**ou **Itanium**. |
| /j [provedor] | Especifica o nome do provedor de impressão. |
| /l [caminho] | Especifica o caminho UNC onde os arquivos de driver de impressora que você está usando estão localizados. |
| /m [modelo] | Especifica o nome do modelo de driver. (Esse valor pode ser especificado no arquivo. inf.) |
| /n [nome] | Especifica o nome da impressora. |
| /q | Executa o comando sem notificações para o usuário. |
| /r [porta] | Especifica o nome da porta. |
| /u | Especifica usar o driver de impressora existente se ele já estiver instalado. |
| /t [#] | Especifica a página de índice com base em zero na qual começar. |
| /v [versão] | Especifica a versão do driver. Se você também não especificar um valor para **/k**, deverá especificar um dos seguintes valores: **tipo 2 – modo kernel** ou **tipo 3-modo de usuário**. |
| /w | solicita ao usuário um driver se o driver não for encontrado no arquivo. inf especificado por **/f**. |
| /Y | Especifica que os nomes de impressora não devem ser gerados automaticamente. |
| /z | Especifica para não compartilhar automaticamente a impressora que está sendo instalada. |
| /K | altera o significado do parâmetro **/h [Architecture]** para aceitar **2** no lugar do **x86**, **3** no lugar de **x64**ou **4** no lugar do **Itanium**. Ele também altera o valor do parâmetro **/v [Version]** para aceitar **2** no lugar do **tipo 2 – Kernel Mode** e **3** no lugar do **tipo 3-User Mode**. |
| /Z | Compartilha a impressora que está sendo instalada. Use apenas com o parâmetro **/If** . |
| /MW [mensagem] | Exibe uma mensagem de aviso para o usuário antes de confirmar as alterações especificadas na linha de comando. |
| /MQ [mensagem] | Exibe uma mensagem de confirmação para o usuário antes de confirmar as alterações especificadas na linha de comando. |
| /W [sinalizadores] | Especifica quaisquer parâmetros ou opções para o assistente para adicionar impressora, o assistente para adicionar driver de impressora e o assistente de instalação de impressora de rede.<p>**r**: permite que os assistentes sejam reiniciados na última página. |
| /G [sinalizadores] | Especifica parâmetros e opções globais que você deseja usar.<p>**w**: suprime os avisos do driver de instalação para o usuário. |

#### <a name="remarks"></a>Comentários

- A palavra-chave **PrintUIEntry** diferencia maiúsculas de minúsculas e você deve inserir a sintaxe para esse comando com a capitalização exata mostrada nos exemplos neste tópico.

- Para obter mais exemplos, em um prompt de comando, digite: **rundll32 printui.dll, PrintUIEntry/?**

## <a name="examples"></a>Exemplos

Para adicionar uma nova impressora remota, printer1, para um computador, CLIENT1, que é visível para a conta de usuário em que esse comando é executado, digite:

```
rundll32 printui.dll PrintUIEntry /in /n\\client1\printer1
```

Para adicionar uma impressora usando o assistente para adicionar impressora e usando um arquivo. inf, InfFile. inf, localizado na unidade c: em INFPath, digite:

```
rundll32 printui.dll PrintUIEntry /ii /f c:\Infpath\InfFile.inf
```

Para excluir uma impressora existente, printer1, em um computador, CLIENT1, digite:

```
rundll32 printui.dll PrintUIEntry /dn /n\\client1\printer1
```

Para adicionar uma conexão de impressora por computador, printer2, para todos os usuários de um computador, Client2, digite (a conexão será aplicada quando um usuário fizer logon):

```
rundll32 printui.dll PrintUIEntry /ga /n\\client2\printer2
```

Para excluir uma conexão de impressora por computador, printer2, para todos os usuários de um computador, Client2, digite (a conexão será excluída quando um usuário fizer logon):

```
rundll32 printui.dll PrintUIEntry /gd /n\\client2\printer2
```

Para exibir as propriedades do servidor de impressão, o Print Server1, digite:

```
rundll32 printui.dll PrintUIEntry /s /t1 /c\\printserver1
```

Para exibir as propriedades de uma impressora, printer3, digite:
```
rundll32 printui.dll PrintUIEntry /p /n\\printer3
```

## <a name="additional-references"></a>Referências adicionais

- [rundll32](rundll32.md)

- [Referência de comando de impressão](print-command-reference.md)
