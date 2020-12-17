---
description: 'Saiba mais sobre: recuperação de floresta do AD-aumentando o valor dos pools RID disponíveis'
title: Recuperação de floresta do AD – gerando pools RID
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.openlocfilehash: fe5498bf5efc940b9a91f214f93f40de670df547
ms.sourcegitcommit: e57536e28902ae52d3040141bbd2aa00e91bbdd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97644686"
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>Recuperação de floresta do AD-aumentando o valor dos pools RID disponíveis

>Aplica-se a: Windows Server 2016, Windows Server 2012 e 2012 R2, Windows Server 2008 e 2008 R2

Use o procedimento a seguir para aumentar o valor dos pools de RID (ID relativa) que o mestre de operações do RID alocará depois que o DC for restaurado. Ao aumentar o valor dos pools RID disponíveis, você pode garantir que nenhum DC aloque um RID para uma entidade de segurança que foi criada após o backup que foi usado para restaurar o domínio.

## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Sobre Active Directory pools RID e rIDAvailablePool

Cada domínio tem um objeto **CN = RID Manager $, CN = System, DC** =< *domain_name*>. Esse objeto tem um atributo chamado **rIDAvailablePool**. Esse valor de atributo mantém o espaço global do RID para um domínio inteiro. O valor é um inteiro grande com partes superior e inferior. A parte superior define o número de entidades de segurança que podem ser alocadas para cada domínio (0x3FFFFFFF ou apenas mais de 1.000.000.000). A parte inferior é o número de RIDs que foram alocados no domínio.

> [!NOTE]
> No Windows Server 2016 e 2012, o número de entidades de segurança que podem ser alocadas é aumentado para quase 2.000.000.000. Para obter mais informações, consulte [Gerenciando a emissão de RID](./managing-rid-issuance.md).

- Valor de exemplo: 4611686014132422708
- Parte inferior: 2100 (início do próximo pool de RID a ser alocado)
- Parte superior: 1073741823 (número total de RIDs que podem ser criados em um domínio)

Quando você aumenta o valor do inteiro grande, aumenta o valor da parte inferior. Por exemplo, se você adicionar 100.000 ao valor de exemplo de 4611686014132422708 para uma soma de 4611686014132522708, a nova parte inferior será 102100. Isso indica que o próximo pool de RIDs que será alocado pelo mestre de RID começará com 102100 em vez de 2100.

### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator"></a>Para aumentar o valor dos pools RID disponíveis usando o ADSIEdit e a calculadora

1. Abra Gerenciador do Servidor, clique em **ferramentas** e clique em **Editor ADSI**.
2. Clique com o botão direito do mouse, selecione **conectar a** e conectar faça o contexto de nomenclatura padrão e clique em **OK**.
   ![Captura de tela que mostra como se conectar ao contexto de nomenclatura padrão](media/AD-Forest-Recovery-Raise-RID-Pool/adsi1.png)
3. Navegue até o seguinte caminho de nome distinto: **CN = RID Manager $, CN = System, DC <domain name> =**.
   ![Captura de tela que mostra como procurar o caminho do nome distinto.](media/AD-Forest-Recovery-Raise-RID-Pool/adsi2.png)
3. Clique com o botão direito do mouse e selecione as propriedades de CN = RID Manager $.
4. Selecione o atributo **rIDAvailablePool**, clique em **Editar** e copie o valor inteiro grande para a área de transferência.
   ![Captura de tela que mostra o atributo rIDAvailablePool selecionado.](media/AD-Forest-Recovery-Raise-RID-Pool/adsi3.png)
5. Inicie a calculadora e, no menu **Exibir** , selecione **modo científico**.
6. Adicione 100.000 ao valor atual.
   ![Captura de tela que mostra onde adicionar 100.000 ao valor atual.](media/AD-Forest-Recovery-Raise-RID-Pool/adsi4.png)
7. Usando Ctrl-c ou o comando **Copy** no menu **Editar** , copie o valor para a área de transferência.
8. Na caixa de diálogo Editar do ADSIEdit, Cole esse novo valor.
   ![ADSI Edit](media/AD-Forest-Recovery-Raise-RID-Pool/adsi5.png)
9. Clique em **OK** na caixa de diálogo e **aplique** na folha de propriedades para atualizar o atributo **rIDAvailablePool** .

### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>Para aumentar o valor dos pools RID disponíveis usando o LDP

1. No prompt de comando, digite o seguinte comando e pressione ENTER: **LDP**
2. Clique em **conexão**, clique em **conectar**, digite o nome do Gerenciador de RID e clique em **OK**.
   ![Captura de tela que mostra onde digitar o nome do Gerenciador de RID.](media/AD-Forest-Recovery-Raise-RID-Pool/ldp1.png)
3. Clique em **conexão**, clique em **associar**, selecione **associar com credenciais** e digite suas credenciais administrativas e clique em **OK**.
   ![Captura de tela que mostra a opção associar com credenciais.](media/AD-Forest-Recovery-Raise-RID-Pool/ldp2.png)
4. Clique em **Exibir**, clique em **árvore** e digite a seguinte caminho de nome distinto: CN = RID Manager $, CN = System, DC = captura de *nome de domínio* 
    ![ que mostra onde você digita o caminho do nome distinto.](media/AD-Forest-Recovery-Raise-RID-Pool/ldp3.png)
5. Clique em **procurar** e em **Modificar**.
6. Adicione 100.000 ao valor **rIDAvailablePool** atual e, em seguida, digite a soma em **valores**.
7. Em **DN**, digite `cn=RID Manager$,cn=System,dc=` *<nome \> de domínio*.
8. Em **Editar atributo de entrada**, digite `rIDAvailablePool` .
9. Selecione **substituir** como a operação e, em seguida, clique em **Enter**.
   ![Captura de tela que mostra a opção Replace.](media/AD-Forest-Recovery-Raise-RID-Pool/ldp4.png)
10. Clique em **executar** para executar a operação. Clique em **fechar**
11. Para validar a alteração, clique em **Exibir**, em **árvore** e digite o seguinte caminho de nome distinto: CN = Gerenciador de RID $, CN = System, DC =*nome de domínio*.   Verifique o atributo **rIDAvailablePool** .
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp5.png)

## <a name="next-steps"></a>Próximas etapas

- [Guia de recuperação de floresta do AD](AD-Forest-Recovery-Guide.md)
- [Recuperação de floresta do AD – Procedimentos](AD-Forest-Recovery-Procedures.md)
