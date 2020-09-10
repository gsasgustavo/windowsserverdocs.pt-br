---
title: rpcping
description: Artigo de referência para o comando RPCPing, que confirma a conectividade RPC entre o computador que está executando o Microsoft Exchange Server e qualquer uma das estações de trabalho de cliente do Microsoft Exchange com suporte na rede.
ms.topic: reference
ms.assetid: 7382aa0d-90fc-47c0-84b3-15f52dd656d0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7351195d8206cb13b334ca3e06ffb794e4a13461
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89641177"
---
# <a name="rpcping"></a>rpcping

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Confirma a conectividade RPC entre o computador que está executando o Microsoft Exchange Server e qualquer uma das estações de trabalho de cliente do Microsoft Exchange com suporte na rede. Esse utilitário pode ser usado para verificar se os serviços do Microsoft Exchange Server estão respondendo às solicitações RPC das estações de trabalho do cliente pela rede.

## <a name="syntax"></a>Sintaxe

```
rpcping [/t <protseq>] [/s <server_addr>] [/e <endpoint>
        |/f <interface UUID>[,majorver]] [/O <interface object UUID]
        [/i <#_iterations>] [/u <security_package_id>] [/a <authn_level>]
        [/N <server_princ_name>] [/I <auth_identity>] [/C <capabilities>]
        [/T <identity_tracking>] [/M <impersonation_type>]
        [/S <server_sid>] [/P <proxy_auth_identity>] [/F <RPCHTTP_flags>]
        [/H <RPC/HTTP_authn_schemes>] [/o <binding_options>]
        [/B <server_certificate_subject>] [/b] [/E] [/q] [/c]
        [/A <http_proxy_auth_identity>] [/U <HTTP_proxy_authn_schemes>]
        [/r <report_results_interval>] [/v <verbose_level>] [/d]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| /t `<protseq>` | Especifica a sequência de protocolo a ser usada. Pode ser uma das sequências de protocolo RPC padrão: ncacn_ip_tcp, ncacn_np ou ncacn_http.<p>Se não for especificado, o padrão será ncacn_ip_tcp. |
| /s `<server_addr>` | Especifica o endereço do servidor. Se não for especificado, o computador local será pingado. |
| /e `<endpoint>` | Especifica o ponto de extremidade para executar ping. Se nenhum for especificado, o mapeador de ponto de extremidade no computador de destino será pingado.<p>Essa opção é mutuamente exclusiva com a opção interface (**/f**). |
| /o `<binding_options>` | Especifica as opções de associação para o Ping RPC. |
| /f `<interface UUID>[,Majorver]` | Especifica a interface para executar ping. Essa opção é mutuamente exclusiva com a opção de ponto de extremidade. A interface é especificada como um UUID.<p>Se o *dos majorver* não for especificado, a versão 1 da interface será procurada.<p>Quando a interface é especificada, o **RPCPing** consultará o mapeador de ponto de extremidade no computador de destino para recuperar o ponto de extremidade para a interface especificada. O mapeador de ponto de extremidade será consultado usando as opções especificadas na linha de comando. |
| /O `<object UUID>` | Especifica o UUID do objeto se a interface tiver registrado um. |
| /i `<#_iterations>` | Especifica o número de chamadas a serem feitas. O padrão é 1. Essa opção é útil para medir a latência de conexão se várias iterações forem especificadas. |
| /u `<security_package_id>` | Especifica o pacote de segurança (provedor de segurança) que o RPC usará para fazer a chamada. O pacote de segurança é identificado como um número ou um nome. Se um número for usado, ele será o mesmo número que na API RpcBindingSetAuthInfoEx. Se você especificar essa opção, deverá especificar um nível de autenticação diferente de *nenhum*. Não há nenhum padrão para essa opção. Se não for especificado, o RPC não usará a segurança para o ping. A lista a seguir mostra os nomes e números. Os nomes não diferenciam maiúsculas de minúsculas:<ul><li>Negociar/9 ou um de nego, Snego ou Negotiate</li><li>NTLM/10 ou NTLM</li><li>SChannel/14 ou SChannel</li><li>Kerberos/16 ou Kerberos</li><li>Kernel/20 ou kernel</li></ul> |
| SRDF `<authn_level>` | Especifica o nível de autenticação a ser usado. Se essa opção for especificada, a ID do pacote de segurança (**/u**) também deverá ser especificada. Se essa opção não for especificada, o RPC não usará a segurança para o ping. Não há nenhum padrão para essa opção. Os valores possíveis são:<ul><li>conectar</li><li>chamada</li><li>PCT</li><li>integridade</li><li>privacidade</li></ul> |
| Opção `<server_princ_name>` | Especifica um nome de entidade de segurança de servidor.<p>Esse campo pode ser usado somente quando o nível de autenticação e o pacote de segurança são selecionados. |
| /I `<auth_identity>` | Permite que você especifique uma identidade alternativa para se conectar ao servidor. A identidade está no formato usuário, domínio, senha. Se o nome de usuário, domínio ou senha tiverem caracteres especiais que podem ser interpretados pelo shell, coloque a identidade entre aspas duplas. Você pode especificar `\*` , em vez da senha, e o RPC solicitará que você insira a senha sem ecoa-la na tela. Se esse campo não for especificado, a identidade do usuário conectado será usada.<p>Esse campo pode ser usado somente quando o nível de autenticação e o pacote de segurança são selecionados. |
| /C `<capabilities>` | Especifica uma bitmask hexadecimal de sinalizadores. Esse campo pode ser usado somente quando o nível de autenticação e o pacote de segurança são selecionados. |
| /T `<identity_tracking>` | Especifica estático ou dinâmico. Se não for especificado, Dynamic será o padrão.<p>Esse campo pode ser usado somente quando o nível de autenticação e o pacote de segurança são selecionados. |
| Opção `<impersonation_type>` | Especifica anônimo, identificar, representar ou delegar. O padrão é Impersonate.<p>Esse campo pode ser usado somente quando o nível de autenticação e o pacote de segurança são selecionados. |
| /S `<server_sid>` | Especifica o SID esperado do servidor.<p>Esse campo pode ser usado somente quando o nível de autenticação e o pacote de segurança são selecionados. |
| /P `<proxy_auth_identity>` | Especifica a identidade a ser autenticada no proxy RPC/HTTP. Tem o mesmo formato que para a opção **/i** . Você deve especificar o pacote de segurança (**/u**), o nível de autenticação (**/a**) e os esquemas de autenticação (**/h**) para usar essa opção. |
| F `<RPCHTTP_flags>` | Especifica os sinalizadores a serem passados para a autenticação de front-end RPC/HTTP. Os sinalizadores podem ser especificados como números ou nomes que os sinalizadores reconhecidos atualmente são:<ul><li>Usar SSL/1 ou SSL ou use_ssl</li><li>Usar primeiro esquema de autenticação/2 ou primeiro ou use_first</li></ul>Você deve especificar o pacote de segurança (**/u**) e o nível de autenticação (**/a**) para usar essa opção. |
| /H `<RPC/HTTP_authn_schemes>` | Especifica os esquemas de autenticação a serem usados para autenticação de front-end RPC/HTTP. Essa opção é uma lista de valores numéricos ou nomes separados por vírgula. Exemplo: básico, NTLM. Os valores reconhecidos são (os nomes não diferenciam maiúsculas de minúsculas):<ul><li>Básico/1 ou básico</li><li>NTLM/2 ou NTLM</li><li>Certificado/65536 ou CERT</li></ul><p>Você deve especificar o pacote de segurança (**/u**) e o nível de autenticação (**/a**) para usar essa opção. |
| /B. `<server_certificate_subject>` | Especifica a entidade do certificado do servidor. Você deve usar SSL para que essa opção funcione.<p>Você deve especificar o pacote de segurança (**/u**) e o nível de autenticação (**/a**) para usar essa opção. |
| /b | Recupera a entidade do certificado do servidor do certificado enviado pelo servidor e a imprime em uma tela ou em um arquivo de log. Válido somente quando a opção somente eco de proxy (/E) e as opções usar SSL são especificadas.<p>Você deve especificar o pacote de segurança (**/u**) e o nível de autenticação (**/a**) para usar essa opção. |
| /R | Especifica o proxy HTTP. Se *nenhum*, o proxy RPC será usado. O valor *padrão* significa usar as configurações do IE em seu computador cliente. Qualquer outro valor será tratado como o proxy HTTP explícito. Se você não especificar esse sinalizador, o valor padrão será assumido, ou seja, as configurações do IE serão verificadas. Esse sinalizador só é válido quando o sinalizador **/e** (somente eco) está habilitado. |
| /E | Restringe o ping somente para o proxy RPC/HTTP. O ping não chega ao servidor. Útil ao tentar estabelecer se o proxy RPC/HTTP está acessível. Para especificar um proxy HTTP, use o sinalizador/R. Se um proxy HTTP for especificado no sinalizador/o, essa opção será ignorada.<p>Você deve especificar o pacote de segurança (**/u**) e o nível de autenticação (**/a**) para usar essa opção. |
| /q | Especifica o modo silencioso. Não emite prompts, exceto senhas. Assume a resposta *Y* a todas as consultas. Use essa opção com cuidado. |
| /c | Usar certificado de cartão inteligente. o RPCPing solicitará ao usuário que escolha cartão inteligente. |
| /A | Especifica a identidade com a qual autenticar para o proxy HTTP. Tem o mesmo formato que para a opção/I.<p>Você deve especificar os esquemas de autenticação (/U), o pacote de segurança (**/u**) e o nível de autenticação (**/a**) para usar essa opção. |
| /U | Especifica os esquemas de autenticação a serem usados para autenticação de proxy HTTP. Essa opção é uma lista de valores numéricos ou nomes separados por vírgula. Exemplo: básico, NTLM. Os valores reconhecidos são (os nomes não diferenciam maiúsculas de minúsculas):<ul><li>Básico/1 ou básico</li><li>NTLM/2 ou NTLM</li></ul>Você deve especificar o pacote de segurança (**/u**) e o nível de autenticação (**/a**) para usar essa opção. |
| /r | Se várias iterações forem especificadas, essa opção fará o **RPCPing** exibir estatísticas de execução atuais periodicamente, em vez da última chamada. O intervalo do relatório é fornecido em segundos. O padrão é 15. |
| /v | Informa ao **RPCPing** como é detalhado para fazer a saída. O valor padrão é 1. 2 e 3 fornecem mais saída do **RPCPing**. |
| /d | Inicia a interface do usuário de diagnóstico de rede RPC. |
| /p | Especifica solicitar credenciais se a autenticação falhar. |
| /? | Exibe a ajuda no prompt de comando. |

## <a name="examples"></a>Exemplos

Para descobrir se o servidor Exchange que você se conecta por meio de RPC/HTTP está acessível, digite:

```
rpcping /t ncacn_http /s exchange_server /o RpcProxy=front_end_proxy /P username,domain,* /H Basic /u NTLM /a connect /F 3
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
