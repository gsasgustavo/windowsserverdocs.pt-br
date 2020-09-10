---
title: bcdedit
description: Artigo de referência para o comando bcdedit, que cria novas lojas, modifica as lojas existentes e adiciona parâmetros de menu de inicialização.
ms.topic: reference
ms.assetid: ab2da47d-3aac-44a0-b7fd-bd9561d61553
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/27/2018
ms.openlocfilehash: b3cd41f3ba1980718a5e2c0a37df470a94f67657
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632977"
---
# <a name="bcdedit"></a>bcdedit

Os arquivos BCD (Dados de Configuração da Inicialização) fornecem um repositório usado para descrever os aplicativos de inicialização e as configurações do aplicativo de inicialização. Os objetos e elementos na loja substituem efetivamente Boot.ini.

BCDEdit é uma ferramenta de linha de comando para gerenciar repositórios BCD. Ele pode ser usado para uma variedade de finalidades, incluindo a criação de novas lojas, a modificação de lojas existentes, a adição de parâmetros de menu de inicialização e assim por diante. O BCDEdit oferece essencialmente a mesma finalidade que Bootcfg.exe em versões anteriores do Windows, mas com duas melhorias importantes:

- Expõe um intervalo maior de parâmetros de inicialização que Bootcfg.exe.

- Melhorou o suporte a scripts.

> [!NOTE]
> São necessários privilégios administrativos para usar BCDEdit para modificar o BCD.

BCDEdit é a principal ferramenta para editar a configuração de inicialização do Windows Vista e versões posteriores do Windows. Ele está incluído na distribuição do Windows Vista na pasta%WINDIR%\System32.

O BCDEdit é limitado aos tipos de dados padrão e é projetado principalmente para executar alterações comuns únicas no BCD. Para operações mais complexas ou tipos de dados não padrão, considere o uso da API (interface de programação de aplicativo) do BCD Instrumentação de Gerenciamento do Windows (WMI) para criar ferramentas personalizadas mais poderosas e flexíveis.

## <a name="syntax"></a>Sintaxe

```
bcdedit /command [<argument1>] [<argument2>] ...
```

### <a name="parameters"></a>Parâmetros

### <a name="general-bcdedit-command-line-options"></a>Opções gerais de linha de comando BCDEdit

| Opção | DESCRIÇÃO |
| ------ | ----------- |
| /? | Exibe uma lista de comandos BCDEdit. Executar esse comando sem um argumento exibe um resumo dos comandos disponíveis. Para exibir a ajuda detalhada para um comando específico, execute **bcdedit/?** `<command>`, em que `<command>` é o nome do comando no qual você está pesquisando mais informações. Por exemplo, **bcdedit/? CreateStore** exibe ajuda detalhada para o comando CreateStore. |

#### <a name="parameters-that-operate-on-a-store"></a>Parâmetros que operam em uma loja

| Opção | Descrição |
| ------ | ----------- |
| /createstore | Cria um novo armazenamento de dados de configuração de inicialização vazio. O repositório criado não é um repositório do sistema. |
| /Export | Exporta o conteúdo do repositório do sistema para um arquivo. Esse arquivo pode ser usado posteriormente para restaurar o estado do repositório do sistema. Esse comando é válido somente para o repositório do sistema. |
| /Import | Restaura o estado do armazenamento do sistema usando um arquivo de dados de backup gerado anteriormente usando a opção **/Export** . Esse comando exclui as entradas existentes no repositório do sistema antes que a importação ocorra. Esse comando é válido somente para o repositório do sistema. |
| /store | Essa opção pode ser usada com a maioria dos comandos BCDedit para especificar o repositório a ser usado. Se essa opção não for especificada, o BCDEdit operará no repositório do sistema. A execução do comando **bcdedit/Store** por si só é equivalente à execução do comando **bcdedit/enum active** . |

#### <a name="parameters-that-operate-on-entries-in-a-store"></a>Parâmetros que operam em entradas em um repositório

| Parâmetro | Descrição |
| ------ | ----------- |
| /Copy | Faz uma cópia de uma entrada de inicialização especificada no mesmo repositório do sistema. |
| /Create | Cria uma nova entrada no repositório de dados de configuração de inicialização. Se um identificador bem conhecido for especificado, os parâmetros **/Application**, **/Inherit**e **/Device** não poderão ser especificados. Se um identificador não for especificado ou não for bem conhecido, uma opção **/Application**, **/Inherit**ou **/Device** deverá ser especificada. |
| /delete | Exclui um elemento de uma entrada especificada. |

#### <a name="parameters-that-operate-on-entry-options"></a>Parâmetros que operam nas opções de entrada

| Parâmetro | Descrição |
| ------ | ----------- |
| /DeleteValue | Exclui um elemento especificado de uma entrada de inicialização. |
| /Set | Define um valor de opção de entrada. |

#### <a name="parameters-that-control-output"></a>Parâmetros que controlam a saída

| Parâmetro | Descrição |
| ------ | ----------- |
| /enum | Lista entradas em um repositório. A opção **/enum** é o valor padrão para BCEdit, portanto, a execução do comando **bcdedit** sem parâmetros é equivalente à execução do comando **bcdedit/enum active** . |
| /v | Modo detalhado. Normalmente, todos os identificadores de entrada conhecidos são representados por sua forma abreviada amigável. A especificação de **/v** como uma opção de linha de comando exibe todos os identificadores em completo. Executar o comando **bcdedit/v** por si só é equivalente a executar o comando **bcdedit/enum active/v** . |

#### <a name="parameters-that-control-the-boot-manager"></a>Parâmetros que controlam o Gerenciador de inicialização

| Parâmetro | Descrição |
| ------ | ----------- |
| /bootsequence | Especifica uma única ordem de exibição a ser usada para a próxima inicialização. Esse comando é semelhante à opção **/DisplayOrder** , exceto que é usado apenas na próxima vez que o computador for iniciado. Posteriormente, o computador reverte para a ordem de exibição original. |
| /default | Especifica a entrada padrão que o Gerenciador de inicialização seleciona quando o tempo limite expira. |
| /displayorder | Especifica a ordem de exibição que o Gerenciador de inicialização usa ao exibir parâmetros de inicialização para um usuário. |
| /Timeout | Especifica o tempo de espera, em segundos, antes que o Gerenciador de inicialização selecione a entrada padrão. |
| /toolsdisplayorder | Especifica a ordem de exibição para o Gerenciador de inicialização usar ao exibir o menu **ferramentas** . |

#### <a name="parameters-that-control-emergency-management-services"></a>Parâmetros que controlam os serviços de gerenciamento de emergência

| Parâmetro | Descrição |
| ------ | ----------- |
| /bootems | Habilita ou desabilita os serviços de gerenciamento de emergência (EMS) para a entrada especificada. |
| /EMS | Habilita ou desabilita o EMS para a entrada de inicialização do sistema operacional especificado. |
| /emssettings | Define as configurações globais do EMS para o computador. o **/emssettings** não habilita ou DESABILITA o EMS para qualquer entrada de inicialização específica. |

#### <a name="parameters-that-control-debugging"></a>Parâmetros que controlam a depuração

| Parâmetro | Descrição |
| ------ | ----------- |
| /bootdebug | Habilita ou desabilita o depurador de inicialização para uma entrada de inicialização especificada. Embora esse comando funcione para qualquer entrada de inicialização, ele só é eficaz para aplicativos de inicialização. |
| /dbgsettings | Especifica ou exibe as configurações globais do depurador para o sistema. Este comando não enablepose. Para definir uma configuração de depurador global individual, use o comando **bcdedit/set** `<dbgsettings> <type> <value>` . |
| /debug | Habilita ou desabilita o depurador de kernel para uma entrada de inicialização especificada. |

## <a name="additional-references"></a>Referências adicionais

Para obter exemplos de como usar BCDEdit, consulte o artigo [referência de opções de bcdedit](/windows-hardware/drivers/devtest/bcd-boot-options-reference) .

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
