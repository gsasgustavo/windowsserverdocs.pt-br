---
title: Como detectar, habilitar e desabilitar SMBv1, SMBv2 e SMBv3 no Windows
description: Descreve como habilitar e desabilitar o protocolo de bloqueio de mensagens do servidor (SMBv1, SMBv2 e SMBv3) em ambientes de cliente e servidor do Windows.
author: Deland-Han
manager: dcscontentpm
ms.topic: how-to
ms.author: delhan
ms.date: 10/29/2020
ms.custom: contperfq2
ms.openlocfilehash: e38bbc5a80f80747ae3cb90c91123d91ed4e5e25
ms.sourcegitcommit: 28b5ab74cb0b40539ccc1a83998d6391e87fe51f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96614948"
---
# <a name="how-to-detect-enable-and-disable-smbv1-smbv2-and-smbv3-in-windows"></a>Como detectar, habilitar e desabilitar SMBv1, SMBv2 e SMBv3 no Windows

>Aplica-se a: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Este artigo descreve como habilitar e desabilitar o SMB (Server Message Block) versão 1 (SMBv1), o SMB versão 2 (SMBv2) e a versão 3 do SMB (SMBv3) nos componentes do cliente e do servidor SMB.

Embora a desabilitação ou a remoção de SMBv1 possa causar alguns problemas de compatibilidade com computadores antigos ou software, o SMBv1 tem vulnerabilidades de segurança significativas e [incentivamos enfaticamente a você não usá-lo](https://techcommunity.microsoft.com/t5/storage-at-microsoft/stop-using-smb1/ba-p/425858).

## <a name="disabling-smbv2-or-smbv3-for-troubleshooting"></a>Desabilitando o SMBv2 ou o SMBv3 para solução de problemas

Embora seja recomendável manter o SMBv2 e o SMBv3 habilitados, talvez você ache útil desabilitar um temporariamente para solução de problemas, conforme descrito em [como detectar o status, habilitar e desabilitar protocolos SMB no servidor SMB](detect-enable-and-disable-smbv1-v2-v3.md#how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-server).

No Windows 10, Windows 8.1 e no Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 e Windows Server 2012, desabilitar o SMBv3 desativa a funcionalidade a seguir (e também a funcionalidade SMBv2 descrita na lista anterior):

- Failover transparente-os clientes reconectam-se sem interrupção para nós de cluster durante a manutenção ou failover
- Scale Out – acesso simultâneo a dados compartilhados em todos os nós de cluster de arquivos 
- Multicanal-agregação de largura de banda de rede e tolerância a falhas se vários caminhos estiverem disponíveis entre o cliente e o servidor
- SMB Direct – adiciona suporte à rede RDMA para um desempenho muito alto, com baixa latência e baixa utilização da CPU
- Criptografia – fornece criptografia de ponta a ponta e protege contra espionagem de redes não confiáveis
- Concessão de diretório-melhora os tempos de resposta do aplicativo em filiais por meio de cache
- Otimizações de desempenho-otimizações para e/s de leitura/gravação aleatórias pequenas

No Windows 7 e no Windows Server 2008 R2, desabilitar o SMBv2 desativa a seguinte funcionalidade:

- Composição de solicitação – permite enviar várias solicitações SMB 2 como uma única solicitação de rede
- Leituras e gravações maiores-melhor uso de redes mais rápidas
- Cache de propriedades de pasta e arquivo – os clientes mantêm cópias locais de pastas e arquivos
- Identificadores duráveis – permitir que a conexão Reconecte-se de forma transparente ao servidor se houver uma desconexão temporária
- Assinatura de mensagem aprimorada-HMAC SHA-256 substitui MD5 como algoritmo de hash
- Escalabilidade aprimorada para compartilhamento de arquivos-o número de usuários, compartilhamentos e arquivos abertos por servidor aumentou consideravelmente
- Suporte para links simbólicos
- Modelo de concessão de oplock de cliente-limita os dados transferidos entre o cliente e o servidor, melhorando o desempenho em redes de alta latência e aumentando a escalabilidade do servidor SMB
- Suporte a MTU grande-para uso completo de Ethernet de 10 Gigabye (GB)
- Eficiência de energia aprimorada-os clientes que têm arquivos abertos em um servidor podem dormir

O protocolo SMBv2 foi introduzido no Windows Vista e no Windows Server 2008, enquanto o protocolo SMBv3 foi introduzido no Windows 8 e no Windows Server 2012. Para obter mais informações sobre os recursos dos recursos SMBv2 e SMBv3, consulte os seguintes artigos:

[Visão geral do Protocolo SMB](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v=ws.11))

[Novidades do SMB](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff625695(v=ws.10))

## <a name="how-to-remove-smb-v1"></a>Como remover o SMB v1

Veja como remover o SMBv1 no Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016 e Windows 2012 R2.

#### <a name="powershell-methods"></a>Métodos do PowerShell

##### <a name="smb-v1-client-and-server"></a>SMB V1 (cliente e servidor)

- Ocorre

  ```PowerShell
  Get-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

- Desativar

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

- Habilitar:

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

#### <a name="windows-server-2012-r2-windows-server-2016-windows-server-2019-server-manager-method-for-disabling-smb"></a>Windows Server 2012 R2, Windows Server 2016, Windows Server 2019: método de Gerenciador do Servidor para desabilitar o SMB

##### <a name="smb-v1"></a>SMB v1

![Método Gerenciador do Servidor-Dashboard](media/detect-enable-and-disable-smbv1-v2-v3-1.png)

#### <a name="windows-81-and-windows-10-powershell-method"></a>Windows 8.1 e Windows 10: método do PowerShell

##### <a name="smb-v1-protocol"></a>Protocolo SMB v1

- Ocorre

  ```PowerShell
  Get-WindowsOptionalFeature –Online –FeatureName SMB1Protocol
  ```

- Desativar

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

- Habilitar:

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

##### <a name="smb-v2v3-protocol-only-disables-smb-v2v3-server"></a>Protocolo SMB V2/V3 (desabilita apenas o servidor SMB V2/V3)

- Ocorre

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- Desativar

  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $false
  ```

- Habilitar:

  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $true
  ```

#### <a name="windows-81-and-windows-10-add-or-remove-programs-method"></a>Windows 8.1 e Windows 10: método adicionar ou remover programas

![Método de cliente de programas de Add-Remove](media/detect-enable-and-disable-smbv1-v2-v3-2.png)

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-server"></a>Como detectar o status, habilitar e desabilitar protocolos SMB no servidor SMB

### <a name="for-windows-8-and-windows-server-2012"></a>Para Windows 8 e Windows Server 2012

O Windows 8 e o Windows Server 2012 apresentam o novo cmdlet **set-SMBServerConfiguration** do Windows PowerShell. O cmdlet permite habilitar ou desabilitar os protocolos SMBv1, SMBv2 e SMBv3 no componente de servidor. 

> [!NOTE]
> Quando você habilita ou desabilita o SMBv2 no Windows 8 ou no Windows Server 2012, o SMBv3 também é habilitado ou desabilitado. Esse comportamento ocorre porque esses protocolos compartilham a mesma pilha.

Você não precisa reiniciar o computador depois de executar o cmdlet **set-SMBServerConfiguration** .

##### <a name="smb-v1-on-smb-server"></a>SMB v1 no servidor SMB

- Ocorre

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB1Protocol
  ```

- Desativar

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $false
  ```

- Habilitar:
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $true
  ```

Para obter mais informações, consulte [armazenamento do servidor na Microsoft](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Stop-using-SMB1/ba-p/425858).
##### <a name="smb-v2v3-on-smb-server"></a>SMB V2/V3 no servidor SMB

- Ocorre

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- Desativar

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $false
  ```

- Habilitar:

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $true
  ```

### <a name="for-windows-7-windows-server-2008-r2-windows-vista-and-windows-server-2008"></a>Para Windows 7, Windows Server 2008 R2, Windows Vista e Windows Server 2008

Para habilitar ou desabilitar os protocolos SMB em um servidor SMB que esteja executando o Windows 7, o Windows Server 2008 R2, o Windows Vista ou o Windows Server 2008, use o Windows PowerShell ou o editor do registro.

#### <a name="powershell-methods"></a>Métodos do PowerShell

> [!NOTE]
> Este método requer o PowerShell 2,0 ou versão posterior do PowerShell.

##### <a name="smb-v1-on-smb-server"></a>SMB v1 no servidor SMB

Ocorre

```PowerShell
Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}
```

Configuração padrão = habilitada (nenhuma chave do registro é criada), portanto, nenhum valor de SMB1 será retornado

Desativar

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 0 –Force
```

Habilitar:

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 1 –Force
```

**Observação** Você deve reiniciar o computador depois de fazer essas alterações.
Para obter mais informações, consulte [armazenamento do servidor na Microsoft](https://techcommunity.microsoft.com/t5/storage-at-microsoft/stop-using-smb1/ba-p/425858).
##### <a name="smb-v2v3-on-smb-server"></a>SMB V2/V3 no servidor SMB

Ocorre

```PowerShell
Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}
```

Desativar

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 0 –Force
```

Habilitar:

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 1 –Force
```

> [!NOTE]
> Você deve reiniciar o computador depois de fazer essas alterações.

#### <a name="registry-editor"></a>Editor do Registro

> [!IMPORTANT]
> Siga as etapas nesta seção com cuidado. Problemas sérios podem ocorrer se você modificar o Registro incorretamente. Antes de modificá-lo, [faça backup do Registro para a restauração](https://support.microsoft.com/help/322756) em caso de problemas.

Para habilitar ou desabilitar o SMBv1 no servidor SMB, configure a seguinte chave do registro:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

```
Registry entry: SMB1
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created)
```

Para habilitar ou desabilitar o SMBv2 no servidor SMB, configure a seguinte chave do registro:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

```
Registry entry: SMB2
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created)
```

> [!NOTE]
> Você deve reiniciar o computador depois de fazer essas alterações.

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-client"></a>Como detectar o status, habilitar e desabilitar protocolos SMB no cliente SMB

### <a name="for-windows-vista-windows-server-2008-windows-7-windows-server-2008-r2-windows-8-and-windows-server-2012"></a>Para Windows Vista, Windows Server 2008, Windows 7, Windows Server 2008 R2, Windows 8 e Windows Server 2012

> [!NOTE]
> Quando você habilita ou desabilita o SMBv2 no Windows 8 ou no Windows Server 2012, o SMBv3 também é habilitado ou desabilitado. Esse comportamento ocorre porque esses protocolos compartilham a mesma pilha.

##### <a name="smb-v1-on-smb-client"></a>SMB v1 no cliente SMB

- Detect

  ```cmd
  sc.exe qc lanmanworkstation
  ```

- Desativar

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= disabled
  ```

- Habilitar:

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= auto
  ```

Para obter mais informações, consulte [armazenamento do servidor na Microsoft](https://techcommunity.microsoft.com/t5/storage-at-microsoft/stop-using-smb1/ba-p/425858)
##### <a name="smb-v2v3-on-smb-client"></a>SMB V2/V3 no cliente SMB

- Ocorre

  ```cmd
  sc.exe qc lanmanworkstation
  ```

- Desativar

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/nsi
  sc.exe config mrxsmb20 start= disabled
  ```

- Habilitar:

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb20 start= auto
  ```

> [!NOTE]
> - Você deve executar esses comandos em um prompt de comandos com privilégios elevados.
> - Você deve reiniciar o computador depois de fazer essas alterações.


## <a name="disable-smbv1-server-with-group-policy"></a>Desabilitar o servidor SMBv1 com Política de Grupo

Este procedimento configura o seguinte novo item no registro:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

- Entrada do registro: **SMB1**
- REG_DWORD: **0** = desabilitado

Para configurar isso usando Política de Grupo, siga estas etapas:

1. Abra o **Console de Gerenciamento de Diretiva de Grupo**. Clique com o botão direito no GPO (Objeto de Diretiva de Grupo) que deve conter o novo item de preferência e clique em **Editar**.

2. Na árvore de console em **configuração do computador**, expanda a pasta **preferências** e expanda a pasta **configurações do Windows** .

3. Clique com o botão direito do mouse no nó **do registro** , aponte para **novo** e selecione **item do registro**.

   ![Registro-item de novo registro](media/detect-enable-and-disable-smbv1-v2-v3-3.png)

Na caixa de diálogo **Propriedades do novo registro**, selecione o seguinte:

- **Ação**: criar
- **Hive**: HKEY_LOCAL_MACHINE
- **Caminho da chave**: SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters
- **Nome do valor**: SMB1
- **Tipo de valor**: REG_DWORD
- **Dados do valor**: 0

![Novas propriedades do registro-geral](media/detect-enable-and-disable-smbv1-v2-v3-4.png)

Isso desabilita os componentes do servidor SMBv1. Esse Política de Grupo deve ser aplicado a todas as estações de trabalho, servidores e controladores de domínio necessários no domínio.

> [!NOTE]
> Os [filtros WMI](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc947846(v=ws.10)) também podem ser definidos para excluir sistemas operacionais sem suporte ou exclusões selecionadas, como o Windows XP.

> [!IMPORTANT]
> Tenha cuidado ao fazer essas alterações nos controladores de domínio nos quais o Windows XP herdado ou os sistemas Linux anteriores e de terceiros (que não dão suporte a SMBv2 ou SMBv3) exigem acesso ao SYSVOL ou a outros compartilhamentos de arquivos em que o SMB v1 está sendo desabilitado.

## <a name="disable-smbv1-client-with-group-policy"></a>Desabilitar o cliente SMBv1 com Política de Grupo

Para desabilitar o cliente SMBv1, a chave do registro de serviços precisa ser atualizada para desabilitar o início de **MRxSMB10** e, em seguida, a dependência em **MRxSMB10** precisa ser removida da entrada para **LanmanWorkstation** para que possa ser iniciada normalmente sem exigir que o **MRxSMB10** seja iniciado pela primeira vez.

Isso atualizará e substituirá os valores padrão nos dois itens a seguir no registro:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\mrxsmb10**

Entrada do registro: **iniciar** REG_DWORD: **4**= desabilitado

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation**

Entrada do registro: **DependOnService** REG_MULTI_SZ: **"Bowser", "MRxSmb20", "NSI"**

> [!NOTE]
> O padrão incluído MRxSMB10, que agora é removido como dependência.

Para configurar isso usando Política de Grupo, siga estas etapas:

1. Abra o **Console de Gerenciamento de Diretiva de Grupo**. Clique com o botão direito no GPO (Objeto de Diretiva de Grupo) que deve conter o novo item de preferência e clique em **Editar**.

2. Na árvore de console em **configuração do computador**, expanda a pasta **preferências** e expanda a pasta **configurações do Windows** .

3. Clique com o botão direito do mouse no nó **do registro** , aponte para **novo** e selecione **item do registro**.

4. Na caixa de diálogo **Propriedades do novo registro** , selecione o seguinte:

   - **Ação**: atualizar
   - **Hive**: HKEY_LOCAL_MACHINE
   - **Caminho da chave**: SYSTEM\CurrentControlSet\services\mrxsmb10
   - **Nome do valor**: iniciar
   - **Tipo de valor**: REG_DWORD
   - **Dados do valor**: 4

   ![Propriedades de início – geral](media/detect-enable-and-disable-smbv1-v2-v3-5.png)

5. Em seguida, remova a dependência do **MRxSMB10** que acabou de ser desabilitada.

   Na caixa de diálogo **Propriedades do novo registro** , selecione o seguinte:

   - **Ação**: substituir
   - **Hive**: HKEY_LOCAL_MACHINE
   - **Caminho da chave**: SYSTEM\CurrentControlSet\Services\LanmanWorkstation
   - **Nome do valor**: DependOnService
   - **Tipo de valor**: REG_MULTI_SZ
   - **Dados do valor**:
      - Bowser
      - MRxSmb20
      - NSI

   > [!NOTE]
   > Essas três cadeias de caracteres não terão marcadores (consulte a captura de tela a seguir).

   ![Propriedades DependOnService](media/detect-enable-and-disable-smbv1-v2-v3-6.png)

   O valor padrão inclui **MRxSMB10** em muitas versões do Windows, portanto, ao substituí-los por essa cadeia de caracteres de vários valores, ele está em vigor, removendo **MRxSMB10** como uma dependência de **LanmanServer** e indo de quatro valores padrão para apenas esses três valores acima.

   > [!NOTE]
   > Ao usar Console de Gerenciamento de Política de Grupo, você não precisa usar aspas ou vírgulas. Basta digitar cada entrada em linhas individuais.

6. Reinicie os sistemas de destino para concluir a desabilitação do SMB v1.

### <a name="auditing-smbv1-usage"></a>Auditoria de uso de SMBv1

Para determinar quais clientes estão tentando se conectar a um servidor SMB com SMBv1, você pode habilitar a auditoria no Windows Server 2016, Windows 10 e Windows Server 2019. Você também pode auditar no Windows 7 e no Windows Server 2008 R2 se eles tiverem instalado a atualização mensal de 2018 de maio e no Windows 8, Windows 8.1, Windows Server 2012 e Windows Server 2012 R2 se tiverem instalado a atualização de julho de 2017 mensal.

- Habilitar:

  ```PowerShell
  Set-SmbServerConfiguration –AuditSmb1Access $true
  ```

- Desativar

  ```PowerShell
  Set-SmbServerConfiguration –AuditSmb1Access $false
  ```

- Ocorre

  ```PowerShell
  Get-SmbServerConfiguration | Select AuditSmb1Access
  ```

Quando a auditoria do SMBv1 estiver habilitada, o evento 3000 aparecerá no log de eventos "Microsoft-Windows-SMBServer\Audit", identificando cada cliente que tenta se conectar com o SMBv1.

### <a name="summary"></a>Resumo

Se todas as configurações estiverem no mesmo objeto de Política de Grupo (GPO), Política de Grupo gerenciamento exibirá as configurações a seguir.

![Editor de Gerenciamento de Política de Grupo registro](media/detect-enable-and-disable-smbv1-v2-v3-7.png)

### <a name="testing-and-validation"></a>Teste e validação

Depois que eles forem configurados, permita que a política seja replicada e atualizada. Conforme necessário para o teste, execute **gpupdate/force** em um prompt de comando e examine os computadores de destino para certificar-se de que as configurações do registro sejam aplicadas corretamente. Verifique se o SMB V2 e o SMB v3 estão funcionando para todos os outros sistemas no ambiente.

> [!NOTE]
> Não se esqueça de reiniciar os sistemas de destino.
