---
description: 'Saiba mais sobre: Apêndice C: contas e grupos protegidos no Active Directory'
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: Apêndice C-contas e grupos protegidos no Active Directory
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a968ddd70aa74d571e939c3d2c21cbc24e572f5e
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711761"
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>Apêndice C: Contas protegidas e grupos no Active Directory

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>Apêndice C: Contas protegidas e grupos no Active Directory

No Active Directory, um conjunto padrão de contas e grupos altamente privilegiados é considerado contas e grupos protegidos. Com a maioria dos objetos no Active Directory, os administradores delegados (usuários que têm permissões delegadas para gerenciar objetos Active Directory) podem alterar as permissões nos objetos, incluindo a alteração de permissões para permitir que eles alterem associações dos grupos, por exemplo.

No entanto, com contas e grupos protegidos, as permissões dos objetos são definidas e impostas por meio de um processo automático que garante que as permissões nos objetos permaneçam consistentes, mesmo se os objetos forem movidos para o diretório. Mesmo que alguém altere manualmente as permissões de um objeto protegido, esse processo garante que as permissões sejam retornadas rapidamente aos seus padrões.

### <a name="protected-groups"></a>Grupos protegidos

A tabela a seguir contém os grupos protegidos no Active Directory listados pelo sistema operacional do controlador de domínio.

#### <a name="protected-accounts-and-groups-in-active-directory-by-operating-system"></a>Contas e grupos protegidos em Active Directory pelo sistema operacional

| Windows Server 2003 RTM | Windows Server 2003 SP1 + | Windows Server 2012, <br> Windows Server 2008 R2, <br> Windows Server 2008 | Windows Server 2016 |
| --- | --- | --- | --- |
|Opers. de contas|Opers. de contas|Opers. de contas|Opers. de contas|
|Administrador|Administrador|Administrador|Administrador|
|Administradores|Administradores|Administradores|Administradores|
|Operadores de cópia|Operadores de cópia|Operadores de cópia|Operadores de cópia|
|Editores de Certificados|||
|Administradores do domínio|Administradores do domínio|Administradores do domínio|Administradores do domínio|
|Controladores de Domínio|Controladores de Domínio|Controladores de Domínio|Controladores de Domínio|
|Administrador corporativo|Administrador corporativo|Administrador corporativo|Administrador corporativo|
|Krbtgt|Krbtgt|Krbtgt|Krbtgt|
|Operadores de Impressão|Operadores de Impressão|Operadores de Impressão|Operadores de Impressão|
|||Controladores de Domínio somente leitura|Controladores de Domínio somente leitura|
|Replicador|Replicador|Replicador|Replicador|
|Administradores de esquemas|Administradores de esquemas|Administradores de esquemas|Administradores de esquemas|
|Operadores de Servidores|Operadores de Servidores|Operadores de Servidores|Operadores de Servidores|

#### <a name="adminsdholder"></a>AdminSDHolder

A finalidade do objeto AdminSDHolder é fornecer permissões de "modelo" para as contas e grupos protegidos no domínio. O AdminSDHolder é criado automaticamente como um objeto no contêiner do sistema de cada domínio Active Directory. Seu caminho é: **CN = AdminSDHolder, CN = System, DC =<domain_component>, DC =<domain_component>?.**

Ao contrário da maioria dos objetos no domínio Active Directory, que pertencem ao grupo Administradores, o AdminSDHolder pertence ao grupo Admins. do domínio. Por padrão, o EAs pode fazer alterações no objeto AdminSDHolder de qualquer domínio, assim como os grupos admins. do domínio do domínio e administradores. Além disso, embora o proprietário padrão do AdminSDHolder seja o grupo Admins do domínio do domínio, os membros de administradores ou administradores corporativos podem apropriar-se do objeto.

#### <a name="sdprop"></a>SDProp

SDProp é um processo que é executado a cada 60 minutos (por padrão) no controlador de domínio que contém o emulador PDC do domínio (PDCE). SDProp compara as permissões no objeto AdminSDHolder do domínio com as permissões nas contas e grupos protegidos no domínio. Se as permissões em qualquer uma das contas e grupos protegidos não corresponderem às permissões no objeto AdminSDHolder, as permissões nas contas e grupos protegidos serão redefinidas para corresponder às do objeto AdminSDHolder do domínio.

Além disso, a herança de permissões é desabilitada em contas e grupos protegidos, o que significa que, mesmo que as contas e os grupos sejam movidos para locais diferentes no diretório, eles não herdam permissões de seus novos objetos pai. A herança é desabilitada no objeto AdminSDHolder para que as alterações de permissão para os objetos pai não alterem as permissões do AdminSDHolder.

##### <a name="changing-sdprop-interval"></a>Alterando o intervalo de SDProp

Normalmente, não é necessário alterar o intervalo no qual o SDProp é executado, exceto para fins de teste. Se você precisar alterar o intervalo de SDProp, em PDCE para o domínio, use regedit para adicionar ou modificar o valor DWORD AdminSDProtectFrequency em HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters.

O intervalo de valores é em segundos de 60 a 7200 (um minuto a duas horas). Para reverter as alterações, exclua a chave AdminSDProtectFrequency, que fará com que SDProp reverta para o intervalo de 60 minutos. Em geral, você não deve reduzir esse intervalo em domínios de produção, pois ele pode aumentar a sobrecarga de processamento do LSASs no controlador de domínio. O impacto desse aumento depende do número de objetos protegidos no domínio.

##### <a name="running-sdprop-manually"></a>Executando SDProp manualmente

Uma abordagem melhor para testar alterações de AdminSDHolder é executar SDProp manualmente, o que faz com que a tarefa seja executada imediatamente, mas não afeta a execução agendada. Executar o SDProp manualmente é executado de forma ligeiramente diferente nos controladores de domínio que executam o Windows Server 2008 e versões anteriores do que estão em controladores de domínio que executam o Windows Server 2012 ou o Windows Server 2008 R2.

Os procedimentos para executar o SDProp manualmente em sistemas operacionais mais antigos são fornecidos no [artigo Suporte da Microsoft 251343](https://support.microsoft.com/kb/251343)e a seguir estão as instruções passo a passo para sistemas operacionais mais antigos e mais recentes. Em ambos os casos, você deve se conectar ao objeto rootDSE em Active Directory e executar uma operação de modificação com um DN nulo para o objeto rootDSE, especificando o nome da operação como o atributo a ser modificado. Para obter mais informações sobre operações modificáveis no objeto rootDSE, consulte [RootDSE Modify Operations](/openspecs/windows_protocols/ms-adts/fc74972f-b267-4c1a-8716-0f5b48cf52b9) no site do MSDN.

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Executando SDProp manualmente no Windows Server 2008 ou anterior

Você pode forçar o SDProp a ser executado usando Ldp.exe ou executando um script de modificação LDAP. Para executar o SDProp usando Ldp.exe, execute as seguintes etapas depois de fazer alterações no objeto AdminSDHolder em um domínio:

1. Iniciar **Ldp.exe**.
2. Clique em **conexão** na caixa de diálogo LDP e clique em **conectar**.

   ![Captura de tela que mostra a opção de menu conectar.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)

3. Na caixa de diálogo **conectar** , digite o nome do controlador de domínio para o domínio que contém a função emulador de PDC (PDCE) e clique em **OK**.

   ![Captura de tela que mostra onde digitar o nome do controlador de domínio para o domínio que contém a função do emulador de PDC (PDCE).](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)

4. Verifique se você se conectou com êxito, conforme indicado por **DN: (RootDSE)** na captura de tela a seguir, clique em **conexão** e clique em **associar**.

   ![Captura de tela que mostra onde selecionar a conexão e, em seguida, selecione associar para verificar se você se conectou com êxito.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)

5. Na caixa de diálogo **associar** , digite as credenciais de uma conta de usuário que tenha permissão para modificar o objeto rootDSE. (Se estiver conectado como esse usuário, você poderá selecionar **associar como** usuário conectado no momento.) Clique em **OK**.

   ![Captura de tela que mostra a caixa de diálogo associar.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)

6. Depois de concluir a operação de ligação, clique em **procurar** e clique em **Modificar**.

   ![Captura de tela que mostra a opção de menu modificar no menu procurar.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)

7. Na caixa de diálogo **Modificar** , deixe o campo **DN** em branco. No campo **Editar atributo de entrada** , digite **FixUpInheritance** e, no campo **valores** , digite **Sim**. Clique em **Enter** para preencher a **lista de entradas** , conforme mostrado na captura de tela a seguir.

   ![Captura de tela que mostra a caixa de diálogo Modificar.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)

8. Na caixa de diálogo Modificar, clique em executar e verifique se as alterações feitas no objeto AdminSDHolder foram exibidas nesse objeto.

> [!NOTE]
> Para obter informações sobre como modificar o AdminSDHolder para permitir contas sem privilégios designadas para modificar a associação de grupos protegidos, consulte o [Apêndice I: Criando contas de gerenciamento para contas e grupos protegidos no Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md).

Se preferir executar o SDProp manualmente via LDIFDE ou um script, você poderá criar uma entrada de modificação, conforme mostrado aqui:

![Captura de tela que mostra como você pode criar uma entrada de modificação.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Executando o SDProp manualmente no Windows Server 2012 ou no Windows Server 2008 R2

Você também pode forçar o SDProp a ser executado usando Ldp.exe ou executando um script de modificação LDAP. Para executar o SDProp usando Ldp.exe, execute as seguintes etapas depois de fazer alterações no objeto AdminSDHolder em um domínio:

1. Iniciar **Ldp.exe**.

2. Na caixa de diálogo **LDP** , clique em **conexão** e em **conectar**.

   ![Captura de tela que mostra a caixa de diálogo LDP.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)

3. Na caixa de diálogo **conectar** , digite o nome do controlador de domínio para o domínio que contém a função emulador de PDC (PDCE) e clique em **OK**.

   ![Captura de tela que mostra a caixa de diálogo Conectar.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)

4. Verifique se você se conectou com êxito, conforme indicado por **DN: (RootDSE)** na captura de tela a seguir, clique em **conexão** e clique em **associar**.

   ![Captura de tela que mostra a opção de menu associar no menu conexão.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)

5. Na caixa de diálogo **associar** , digite as credenciais de uma conta de usuário que tenha permissão para modificar o objeto rootDSE. (Se estiver conectado como esse usuário, você poderá selecionar **associar como usuário conectado no momento**.) Clique em **OK**.

   ![Captura de tela que mostra onde digitar as credenciais de uma conta de usuário que tem permissão para modificar o objeto rootDSE.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)

6. Depois de concluir a operação de ligação, clique em **procurar** e clique em **Modificar**.

   ![contas e grupos protegidos](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)

7. Na caixa de diálogo **Modificar** , deixe o campo **DN** em branco. No campo **Editar atributo de entrada** , digite **RunProtectAdminGroupsTask** e, no campo **valores** , digite **1**. Clique em **Enter** para preencher a lista de entradas, conforme mostrado aqui.

   ![Captura de tela que mostra o campo editar atributo de entrada.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)

8. Na caixa de diálogo **Modificar** , clique em **executar** e verifique se as alterações feitas no objeto AdminSDHolder foram exibidas nesse objeto.

Se preferir executar o SDProp manualmente via LDIFDE ou um script, você poderá criar uma entrada de modificação, conforme mostrado aqui:

![Captura de tela que mostra o que fazer se você preferir executar o SDProp manualmente por meio de LDIFDE ou um script.](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)
