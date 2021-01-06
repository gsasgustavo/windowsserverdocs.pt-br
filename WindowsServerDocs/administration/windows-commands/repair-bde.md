---
title: repair-bde
description: Artigo de referência para o comando Repair-bde, que pode tentar reconstruir partes críticas de uma unidade seriamente danificada e recuperar dados recuperáveis se a unidade tiver sido criptografada usando o BitLocker.
ms.topic: reference
ms.assetid: 534dca1a-05f7-4ea8-ac24-4fe5f14f988a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b7eb1128a34f366d5a096558118f43473252c8d4
ms.sourcegitcommit: 029b1e19ce11160d5f988046e04a83e8ab5a60dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97904081"
---
# <a name="repair-bde"></a>repair-bde

Tenta reconstruir partes críticas de uma unidade severamente danificada e recuperar dados recuperáveis se a unidade tiver sido criptografada usando o BitLocker e se tiver uma senha ou chave de recuperação válida para descriptografia.

> [!IMPORTANT]
> Se os dados de metadados do BitLocker na unidade estiverem corrompidos, você deverá ser capaz de fornecer um pacote de chave de backup além da senha de recuperação ou da chave de recuperação. Se você usou a configuração de backup de chave padrão para Active Directory Domain Services, é feito o backup do pacote de chave aqui. Você pode usar o [Visualizador BitLocker: Use a senha de recuperação do BitLocker](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-recovery-password-viewer) para obter o pacote de chaves do AD DS.
>
> Usando o pacote de chaves e a senha de recuperação ou a chave de recuperação, você pode descriptografar partes de uma unidade protegida pelo BitLocker, mesmo que o disco esteja corrompido. Cada pacote de chave funciona apenas para uma unidade com o identificador de unidade correspondente.

## <a name="syntax"></a>Syntax

```
repair-bde <inputvolume> <outputvolumeorimage> [-rk] [–rp] [-pw] [–kp] [–lf] [-f] [{-?|/?}]
```

> [!WARNING]
> O conteúdo do volume de saída será **completamente excluído e substituído** pelo conteúdo descriptografado da unidade danificada do BitLocker. Se você quiser salvar os dados existentes na unidade de destino selecionada, mova os dados existentes para outra mídia de backup confiável primeiro, antes de executar o `repair-bde` comando.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| `<inputvolume>` | Identifica a letra da unidade da unidade criptografada pelo BitLocker que você deseja reparar. A letra da unidade deve incluir dois-pontos; por exemplo: **C:**. Se o caminho para um pacote de chaves não for especificado, esse comando pesquisará a unidade em busca de um pacote de chaves. Caso o disco rígido esteja danificado, esse comando pode não ser capaz de localizar o pacote e solicitará que você forneça o caminho. |
| `<outputvolumeorimage>` | Identifica a unidade na qual armazenar o conteúdo da unidade reparada. Todas as informações na unidade de saída serão substituídas. |
| -r | Identifica o local da chave de recuperação que deve ser usada para desbloquear o volume. Esse comando também pode ser especificado como **-RecoveryKey**. |
| -RP | Identifica a senha de recuperação numérica que deve ser usada para desbloquear o volume. Esse comando também pode ser especificado como **-RecoveryPassword**. |
| -PW | Identifica a senha que deve ser usada para desbloquear o volume. Este comando também pode ser especificado como **senha** |
| -KP | Identifica o pacote de chave de recuperação que pode ser usado para desbloquear o volume. Esse comando também pode ser especificado como **-KeyPackage**. |
| -lf | Especifica o caminho para o arquivo que armazenará mensagens de erro, aviso e informações de reparo do bde. Esse comando também pode ser especificado como **-logfile**. |
| -f | Força a desmontagem de um volume mesmo que ele não possa ser bloqueado. Esse comando também pode ser especificado como **-Force**. |
| -? ou/? | Exibe a ajuda no prompt de comando. |

### <a name="limitations"></a>Limitações

As seguintes limitações existem para este comando:

- Esse comando não pode reparar uma unidade que falhou durante o processo de criptografia ou descriptografia.

- Esse comando pressupõe que, se a unidade tiver alguma criptografia, a unidade terá sido totalmente criptografada.

## <a name="examples"></a>Exemplos

Para tentar reparar a unidade C:, para gravar o conteúdo da unidade C: para a unidade D: usando o arquivo de chave de recuperação (RecoveryKey. Bek) armazenado na unidade F:, e para gravar os resultados dessa tentativa no arquivo de log (log.txt) na unidade Z:, digite:

```
repair-bde C: D: -rk F:\RecoveryKey.bek –lf Z:\log.txt
```

Para tentar reparar a unidade C: e gravar o conteúdo da unidade C: para a unidade D: usando a senha de recuperação de 48 dígitos especificada, digite:

```
repair-bde C: D: -rp 111111-222222-333333-444444-555555-666666-777777-888888
```

> [!NOTE]
> A senha de recuperação deve ser digitada em oito blocos de seis dígitos com um hífen separando cada bloco.

Para forçar a desmontagem da unidade C:, tentar reparar a unidade C: e, em seguida, gravar o conteúdo da unidade C: para a unidade D: usando o pacote de chave de recuperação e o arquivo de chave de recuperação (RecoveryKey. Bek) armazenados na unidade F:, digite:

```
repair-bde C: D: -kp F:\RecoveryKeyPackage -rk F:\RecoveryKey.bek -f
```

Para tentar reparar a unidade C: e gravar o conteúdo da unidade C: na unidade D:, em que você deve digitar uma senha para desbloquear a unidade C: (quando solicitado), digite:

```
repair-bde C: D: -pw
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
