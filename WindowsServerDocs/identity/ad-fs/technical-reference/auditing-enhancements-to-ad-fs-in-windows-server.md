---
description: 'Saiba mais sobre: aprimoramentos de auditoria para AD FS no Windows Server 2016'
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: Aprimoramentos de auditoria para o AD FS no Windows Server 2016
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.openlocfilehash: 4254fe1e9e95fbd72fbea049bf6575f76e4b578c
ms.sourcegitcommit: 6a62d736e4d9989515c6df85e2577662deb042b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98103828"
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Aprimoramentos de auditoria para o AD FS no Windows Server 2016

Atualmente, no AD FS para Windows Server 2012 R2, há inúmeros eventos de auditoria gerados para uma única solicitação, e as informações relevantes sobre uma atividade de emissão de log ou de entrada estão ausentes (em algumas versões do AD FS) ou espalhadas por vários eventos de auditoria. Por padrão, os eventos de auditoria do AD FS são desativados devido à sua natureza detalhada.

Com o lançamento do AD FS no Windows Server 2016, a auditoria tornou-se mais simplificada e menos detalhada.

## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Níveis de auditoria no AD FS para Windows Server 2016
Por padrão, AD FS no Windows Server 2016 tem auditoria básica habilitada.  Com a auditoria básica, os administradores verão 5 ou menos eventos para uma única solicitação.  Isso marca uma diminuição significativa no número de eventos que os administradores precisam examinar para ver uma única solicitação.   O nível de auditoria pode ser gerado ou reduzido usando o cmdlet do PowerShell: Set-AdfsProperties-AuditLevel.  A tabela a seguir explica os níveis de auditoria disponíveis.

| Nível de Auditoria | Sintaxe do PowerShell | Descrição |
|--|--|--|
| Nenhum | Set-AdfsProperties-AuditLevel None | A auditoria está desabilitada e nenhum evento será registrado. |
| Básico (padrão) | Set-AdfsProperties-AuditLevel básico | Não mais de 5 eventos serão registrados em log para uma única solicitação |
| Detalhado | Set-AdfsProperties-AuditLevel detalhado | Todos os eventos serão registrados em log.  Isso registrará uma quantidade significativa de informações por solicitação. |

Para exibir o nível de auditoria atual, você pode usar o cmdlet do PowerShell: Get-Adfsproperties.

![Captura de tela que mostra como usar o cmdlet Get-AdfsProperties.](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)

O nível de auditoria pode ser gerado ou reduzido usando o cmdlet do PowerShell: Set-AdfsProperties-AuditLevel.

![Aprimoramentos de auditoria](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)

## <a name="types-of-audit-events"></a>Tipos de eventos de auditoria
AD FS eventos de auditoria podem ser de tipos diferentes, com base nos diferentes tipos de solicitações processadas pelo AD FS. Cada tipo de evento de auditoria tem dados específicos associados a ele.  O tipo de eventos de auditoria pode ser diferenciado entre solicitações de logon (ou seja, solicitações de token) versus solicitações do sistema (chamadas de servidor-servidor, incluindo a busca de informações de configuração).

A tabela a seguir descreve os tipos básicos de eventos de auditoria.

| Tipo de evento de auditoria | ID do evento | Descrição |
|--|--|--|
| Êxito na validação da credencial | 1202 | Uma solicitação em que as novas credenciais são validadas com êxito pelo Serviço de Federação. Isso inclui WS-Trust, WS-Federation, SAML-P (primeiro trecho para gerar SSO) e os pontos de extremidade de autorização OAuth. |
| Novo erro de validação de credencial | 1203 | Uma solicitação na qual a nova validação de credencial falhou no Serviço de Federação. Isso inclui WS-Trust, WS-enalimentate, SAML-P (primeiro segmento para gerar SSO) e os pontos de extremidade de autorização do OAuth. |
| Êxito do token de aplicativo | 1200 | Uma solicitação em que um token de segurança é emitido com êxito pelo Serviço de Federação. Para o WS-Federation, SAML-P isso é registrado quando a solicitação é processada com o artefato de SSO. (como o cookie de SSO). |
| Falha no token do aplicativo | 1201 | Uma solicitação em que a emissão de token de segurança falhou na Serviço de Federação. Para o WS-Federation, SAML-P isso é registrado quando a solicitação foi processada com o artefato de SSO. (como o cookie de SSO). |
| Êxito na solicitação de alteração de senha | 1204 | Uma transação em que a solicitação de alteração de senha foi processada com êxito pelo Serviço de Federação. |
| Erro de solicitação de alteração de senha | 1205 | Uma transação em que a solicitação de alteração de senha não pôde ser processada pelo Serviço de Federação. |
| Sair do sucesso | 1206 | Descreve uma solicitação de saída bem-sucedida. |
| Falha ao sair | 1207 | Descreve uma solicitação de saída com falha. |
