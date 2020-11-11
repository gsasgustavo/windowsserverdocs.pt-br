---
title: Cadeias de caracteres e localização no centro de administração do Windows
description: Saiba mais sobre como preparar suas cadeias de caracteres para localização no SDK do centro de administração do Windows (projeto Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: a59e6e1d12844e809f5e4d9f85109c601dabfe26
ms.sourcegitcommit: b39ea3b83280f00e5bb100df0dc8beaf1fb55be2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94520489"
---
# <a name="strings-and-localization-in-windows-admin-center"></a>Cadeias de caracteres e localização no centro de administração do Windows #

>Aplica-se a: Windows Admin Center, Versão prévia do Windows Admin Center

Vamos aprofundar-se no SDK de extensões do centro de administração do Windows e falar sobre cadeias de caracteres e localização.

Para habilitar a localização de todas as cadeias de caracteres que são renderizadas na camada de apresentação, aproveite o arquivo Strings. resjson em/src/Resources/Strings-já está configurada. Quando você precisar adicionar uma nova cadeia de caracteres à sua extensão, adicione-a a este arquivo resjson como uma nova entrada. A estrutura existente segue este formato:

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

Você pode usar qualquer formato que desejar para as cadeias de caracteres, mas lembre-se de que o processo de geração (o processo que usa o resjson e gera a classe TypeScript utilizável) converte sublinhado (_) em pontos (.).

Por exemplo, esta entrada:
``` ts
"HelloWorld_cim_title": "CIM Component",
```
Gera a seguinte estrutura de acessador:
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```

## <a name="add-other-languages-for-localization"></a>Adicionar outros idiomas para localização ##

Para localização em outros idiomas, um arquivo String. resjson precisa ser criado para cada idioma. Esses arquivos precisam ser colocados no ```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson``` . Os idiomas disponíveis com pastas correspondentes são:

| Idioma      | Pasta      |
| ------------- |-------------|
| Čeština | cs-CZ |
| Deutsch | de-DE |
| Inglês | en-US |
| Español | es-ES |
| Français | fr-FR |
| Magyar | hu-HU |
| Italiano | it-IT |
| 日本語 | ja-JP |
| 한국어 | ko-KR |
| Nederlands | nl-NL |
| Polski | pl-PL |
| Português (Brasil) | pt-BR |
| Português (Portugal) | pt-PT |
| Русский | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文(简体) | zh-CN |
| 中文(繁體) | zh-TW |
> [!NOTE]
> Se suas necessidades de estrutura de arquivo forem diferentes dentro de Loc/saída, você precisará ajustar o localeOffset para a tarefa Gulp ' Generate-resjson-JSON-localizada ' que está na gulpfile.js. Esse deslocamento é a profundidade da pasta Loc que deve começar a Pesquisar arquivos. resjson de cadeias de caracteres.

Cada arquivo Strings. resjson será formatado da mesma maneira como mencionado anteriormente na parte superior deste guia.

Por exemplo, para incluir uma localização para espanhol, inclua essa entrada em ```\loc\output\HelloWorld\es-ES\strings.resjson``` :
```json
"HelloWorld_cim_title": "CIM Componente",
```
Sempre que você adicionar cadeias de caracteres localizadas, a geração de Gulp deverá ser executada novamente para que apareçam. Execute:
``` cmd
gulp generate
```

Para confirmar que as cadeias de caracteres foram geradas, navegue até ```\src\app\assets\strings\{!LanguageFolder}\strings.resjson``` . Sua entrada recém-adicionada aparecerá neste arquivo.
Agora, se você alternar a opção de idioma no centro de administração do Windows, poderá ver as cadeias de caracteres localizadas em sua extensão.
