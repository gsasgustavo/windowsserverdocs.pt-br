---
title: Referência de ferramentas administrativas e tipos de logon – Windows Server
description: Identificar o risco de exposição da credencial associada a diferentes ferramentas administrativas
ms.topic: reference
ms.date: 12/15/2020
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 9b3457cf489e11ce7ede4e0965ec8555102754ec
ms.sourcegitcommit: 4bbb284c909b91cc02b5988b28056f976bc2ca6a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97676071"
---
# <a name="administrative-tools-and-logon-types"></a>Ferramentas administrativas e tipos de logon

Essas informações de referência são fornecidas para ajudar a identificar o risco de exposição de credencial associada a diferentes ferramentas administrativas para administração remota.

Em um cenário de administração remota, as credenciais sempre são expostas no computador de origem. Por isso, recomendamos sempre uma PAW (Estação de trabalho com acesso privilegiado) confiável para contas confidenciais ou de alto impacto. A exposição das credenciais a possíveis roubos no computador de destino (remoto) dependem principalmente do tipo de logon do Windows usado pelo método de conexão.

Esta tabela inclui orientações para as ferramentas administrativas e métodos de conexão mais comuns:

|Método de conexão|Tipo de logon|Credenciais reutilizáveis no destino|Comentários|
|-----------|-------|--------------------|------|
|Logon no console|Interactive (Interativo)|v|Inclui o acesso remoto do hardware/placas lights-out e KVMs de rede.|
|RUNAS|Interactive (Interativo)|v||
|RUNAS /NETWORK|NewCredentials|v|Clona a sessão atual do LSA para acesso local, mas usa novas credenciais ao se conectar aos recursos da rede.|
|Área de Trabalho Remota (sucesso)|RemoteInteractive|v|Se o cliente de Área de Trabalho Remota estiver configurado para compartilhar dispositivos e recursos locais, esses últimos podem ficar comprometidos também.|
|Área de Trabalho Remota (falha: tipo de logon negado)|RemoteInteractive|-|Por padrão, se o logon do RDP falhar, as credenciais serão armazenadas apenas rapidamente. Esse pode não ser o caso se o computador estiver comprometido.|
|Uso da rede * \\\SERVER|Rede|-||
|Uso da rede * \\\SERVER /u:user|Rede|-||
|Snap-ins do MMC para um computador remoto|Rede|-|Exemplo: Gerenciamento de Computador, Visualizador de Eventos, Gerenciador de Dispositivos, Serviços|
|PowerShell WinRM|Rede|-|Exemplo: Enter-PSSession server|
|PowerShell WinRM com CredSSP|NetworkClearText|v|New-PSSession server<br />-Credssp de autenticação<br />-Credencial cred|
|PsExec sem credenciais explícitas|Rede|-|Exemplo: PsExec \\\server cmd|
|PsExec com credenciais explícitas|Rede + interativo|v|PsExec \\\server -u user -p pwd cmd<br />Cria várias sessões de logon.|
|Registro Remoto|Rede|-||
|Gateway de Área de Trabalho Remota|Rede|-|Autenticação em Gateway de Área de Trabalho Remota.|
|Tarefa agendada|Batch|v|A senha também será salva como um segredo LSA em disco.|
|Executar ferramentas como um serviço|Serviço|v|A senha também será salva como um segredo LSA em disco.|
|Scanners de vulnerabilidade|Rede|-|A maioria dos scanners assumem o uso padrão de logons de rede, embora alguns fornecedores possam implementar logons de fora da rede e apresentar mais risco de roubo de credenciais.|

Para autenticação na Web, use a referência da tabela abaixo:

|Método de conexão|Tipo de logon|Credenciais reutilizáveis no destino|Comentários|
|-----------|-------|--------------------|------|
|"Autenticação básica" de IIS|NetworkCleartext<br />(IIS 6.0+)<p>Interactive (Interativo)<br />(antes do IIS 6.0)|v||
|“Autenticação Integrada do Windows” do IIS|Rede|-|Provedores de Kerberos e NTLM.|

Definições de coluna:

- **Tipo de logon**: identifica o tipo de logon iniciado pela conexão.
- **Credenciais reutilizáveis no destino**: indica que os seguintes tipos de credenciais serão armazenados na memória do processo LSASS no computador de destino no qual a conta especificada está conectada localmente:
   - Hashes LM e NT
   - TGTs de Kerberos
   - Senha de texto sem formatação (se for aplicável).

Os símbolos nesta tabela são definidos da seguinte forma:

- (-) indica quando as credenciais não são expostas.
- (v) indica quando as credenciais são expostas.

Para os aplicativos de gerenciamento que não estão nessa tabela, você pode determinar o tipo de logon no campo tipo de logon nos eventos de logon de auditoria. Para saber mais, consulte [Eventos de logon de auditoria](/previous-versions/windows/it-pro/windows-server-2003/cc787567(v=ws.10)).

Em computadores baseados em Windows, todas as autenticações são processadas como um dos vários tipos de logon, independentemente de qual protocolo de autenticação ou autenticador é usado. Essa tabela inclui os tipos mais comuns de logon e seus atributos em relação ao roubo de credenciais:

|Tipo de logon|#|Autenticadores aceitos|Credenciais reutilizáveis na sessão de LSA|Exemplos|
|-------|---|--------------|--------------------|------|
|Interativo (também conhecido como logon local)|2|Senha, Cartão inteligente,<br />outros|Sim|Logon no console;<br />RUNAS;<br />Soluções de controle remoto de hardware (como KVM de rede ou Acesso remoto/Cartão lights-out no servidor)<br />Autenticação básica do IIS (antes do IIS 6.0)|
|Rede|3|Senha,<br />Hash de NT,<br />Tíquete Kerberos|Não (exceto se a delegação estiver habilitada, nesse caso, os tíquetes do Kerberos estarão presentes)|NET USE;<br />Chamadas RPC;<br />Registro Remoto;<br />Autenticação Windows integrada ao IIS;<br />Autenticação Windows do SQL;|
|Batch|4|Senha (armazenada como um segredo de LSA)|Sim|Tarefas Agendadas|
|Serviço|5|Senha (armazenada como um segredo de LSA)|Sim|Serviços Windows|
|NetworkCleartext|8|Senha|Sim|Autenticação básica do IIS (IIS 6.0 e mais recente);<br />Windows PowerShell com CredSSP|
|NewCredentials|9|Senha|Sim|RUNAS /NETWORK|
|RemoteInteractive|10|Senha, Cartão inteligente,<br />outros|Sim|Área de Trabalho Remota (anteriormente conhecida como "Serviços de Terminal")|

Definições de coluna:

- **Tipo de logon**: o tipo de logon solicitado.
- **#** : o identificador numérico para o tipo de logon relatado nos eventos de auditoria no log de eventos de Segurança.
- **Autenticadores aceitos**: indica quais tipos de autenticadores podem iniciar um logon desse tipo.
- **Credenciais reutilizáveis na sessão LSA**: indica se o tipo de logon resulta no armazenamento de credenciais pela sessão LSA, como senhas de texto sem formatação, hashes de NT ou tíquetes Kerberos que podem ser usados para autenticação em outros recursos de rede.
- **Exemplos**: lista de cenários comuns nos quais o tipo de logon é usado.

> [!NOTE]
> Para saber mais sobre tipos de logon, consulte [Enumeração SECURITY_LOGON_TYPE](/windows/win32/api/ntsecapi/ne-ntsecapi-security_logon_type).

**Próximas etapas**

[Planejamento e design do AD DS](../ad-ds/plan/AD-DS-Design-and-Planning.md)
