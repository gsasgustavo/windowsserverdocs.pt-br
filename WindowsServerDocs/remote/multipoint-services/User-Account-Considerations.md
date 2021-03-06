---
title: Considerações sobre conta de usuário
description: Fornece considerações de conta de usuário, nome de usuário e senha para serviços do MultiPoint
ms.topic: article
ms.assetid: e225900b-cee9-48c9-b21c-394dc5e72b78
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 10e58dcf21c9878ec632eee9160a0d3add4a6958
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951501"
---
# <a name="user-account-considerations"></a>Considerações sobre conta de usuário
Este tópico descreve problemas que você, como usuário administrativo, deve considerar ao criar e gerenciar contas de usuário. Você gerencia contas de usuário na guia usuários no MultiPoint Manager. Para obter mais informações, consulte o tópico [Gerenciar contas de usuário](Manage-User-Accounts.md).

## <a name="user-account-types"></a>Tipos de conta de usuário
Uma conta de usuário é uma coleção de informações que informa aos serviços do MultiPoint quais arquivos e pastas um usuário pode acessar, quais alterações eles podem fazer no sistema de serviços do MultiPoint e as preferências de cada usuário, como o plano de fundo da área de trabalho. Cada pessoa acessa sua própria conta de usuário usando um nome de usuário exclusivo e uma senha. Os serviços do MultiPoint dão suporte a três tipos de contas de usuário:

-   **As contas de usuário administrativo** são para indivíduos que usarão o MultiPoint Manager para usar e gerenciar o sistema de serviços do MultiPoint. Para obter mais informações, consulte [Criar uma conta de usuário administrativo](Create-an-Administrative-User-Account.md).

-   **Contas de usuário padrão** são para aqueles que acessarão regularmente estações, mas não gerenciarão o sistema. Normalmente, você deve criar contas de usuário padrão para a maioria dos usuários de sistema MultiPoint Services. Para obter mais informações, consulte [Criar uma conta de usuário padrão](Create-a-Standard-User-Account.md).

-   **Contas de usuário do MultiPoint Dashboard** são para aqueles que usam o MultiPoint Dashboard para gerenciar sessões do usuário padrão e que podem fazer logon de qualquer estação. Para obter mais informações, consulte [Criar uma conta de usuário do MultiPoint Dashboard](Create-a-MultiPoint-Dashboard-User-Account.md).

## <a name="user-name-and-password-considerations"></a>Considerações sobre nome de usuário e senha
Usuários administrativos podem executar tarefas que afetam todos os outros usuários do sistema MultiPoint Services, como instalar software ou alterar as configurações de segurança. Por esse motivo, os usuários administrativos devem ter nomes de usuário exclusivos e senhas que só eles saibam.

Uma consideração importante de contas de usuário é que cada conta de usuário é alocada a uma única biblioteca **Documentos** no Windows Explorer que inclui a pasta **Meus documentos**. Se os usuários padrão em seu sistema MultiPoint Services armazenarem documentos particulares em sua biblioteca **Documentos** no Windows Explorer, eles também deverão fazer logon no sistema MultiPoint Services usando um nome de usuário exclusivo e uma senha que só eles saibam. Para obter mais informações sobre como armazenar documentos no Windows Explorer, consulte o tópico [Gerenciar arquivos do usuário](Manage-User-Files.md).

> [!TIP]
> Para maior segurança do sistema, as senhas de todos os usuários devem ser senhas fortes. Uma senha forte é aquela que não pode ser facilmente adivinhada ou quebrada, tem pelo menos oito caracteres de comprimento, não contém todo ou parte do nome da conta do usuário e contém pelo menos três das quatro categorias de caracteres a seguir: caracteres maiúsculos, caracteres minúsculos, números e símbolos encontrados em um teclado (como!, @, #).

## <a name="see-also"></a>Consulte Também
[Criar uma conta](Create-an-Administrative-User-Account.md) 
 de usuário administrativo [Criar uma conta](Create-a-Standard-User-Account.md) 
 de usuário padrão [Gerenciar arquivos](Manage-User-Files.md) 
 do usuário [Gerenciar contas de usuário](Manage-User-Accounts.md)