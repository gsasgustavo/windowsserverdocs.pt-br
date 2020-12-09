---
title: Criar Plug-ins com o Modelo de Avaliação de Risco do AD FS 2019
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 05/05/2020
ms.topic: article
ms.openlocfilehash: ece40ea47c78c1d45cf55ff9daec551d940276e1
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96865145"
---
# <a name="build-plug-ins-with-ad-fs-2019-risk-assessment-model"></a>Criar Plug-ins com o Modelo de Avaliação de Risco do AD FS 2019

Agora você pode criar seus próprios plug-ins para bloquear ou atribuir uma pontuação de risco às solicitações de autenticação durante vários estágios – solicitação recebida, pré-autenticação e pós-autenticação. Isso pode ser feito usando o novo modelo de avaliação de riscos introduzido com o AD FS 2019.

## <a name="what-is-the-risk-assessment-model"></a>O que é o modelo de avaliação de risco?

O modelo de avaliação de riscos é um conjunto de interfaces e classes que permitem aos desenvolvedores ler cabeçalhos de solicitação de autenticação e implementar sua própria lógica de avaliação de riscos. O código implementado (plug-in) é executado em linha com AD FS processo de autenticação. Por exemplo, usando as interfaces e classes incluídas com o modelo, você pode implementar o código para bloquear ou permitir a solicitação de autenticação com base no endereço IP do cliente incluído no cabeçalho da solicitação. AD FS executará o código para cada solicitação de autenticação e tomará a ação apropriada de acordo com a lógica implementada.

O modelo permite o código de plug-in em qualquer um dos três estágios de AD FS pipeline de autenticação, conforme mostrado abaixo

![modelo](media/ad-fs-risk-assessment-model/risk1.png)

1.    **Estágio de solicitação recebida** – habilita a criação de plug-ins para permitir ou bloquear solicitações quando AD FS recebe a solicitação de autenticação, ou seja, antes de o usuário inserir as credenciais. Você pode usar o contexto da solicitação (por exemplo, IP do cliente, método http, DNS do servidor proxy, etc.) disponível neste estágio para executar a avaliação de risco. Por exemplo, você pode criar um plug-in para ler o IP do contexto da solicitação e bloquear a solicitação de autenticação se o IP estiver na lista predefinida de IPs arriscados.

2.    **Estágio pré-autenticação** – permite a criação de plug-ins para permitir ou bloquear solicitações no ponto em que o usuário fornece as credenciais, mas antes de AD FS as avalia. Neste estágio, além do contexto de solicitação, você também tem informações sobre o contexto de segurança (por exemplo, token de usuário, identificador de usuário, etc.) e o contexto de protocolo (por exemplo, protocolo de autenticação, ClientID, ResourceId, etc.) para usar em sua lógica de avaliação de risco. Por exemplo, você pode criar um plug-in para evitar ataques de irrigação de senha lendo a senha do usuário do token de usuário e bloqueando a solicitação de autenticação se a senha estiver na lista predefinida de senhas arriscadas.

3.    **Pós-autenticação** – habilita a criação de plug-ins para avaliar o risco depois que o usuário forneceu credenciais e AD FS realizou a autenticação. Nesse estágio, além do contexto de solicitação, do contexto de segurança e do contexto de protocolo, você também tem informações sobre o resultado da autenticação (êxito ou falha). O plug-in pode avaliar a pontuação de risco com base nas informações disponíveis e passar a pontuação de risco às regras de declaração e política para obter mais avaliação.

Para entender melhor como criar um plug-in de avaliação de risco e executá-lo em linha com AD FS processo, vamos criar um plug-in de exemplo que bloqueie as solicitações provenientes de determinados IPS de **extranet** identificados como arriscados, registre o plug-in com AD FS e, por fim, teste a funcionalidade.

>[!NOTE]
>Como alternativa, você pode criar um [plug-in de usuário arriscado](https://github.com/microsoft/adfs-sample-block-user-on-adfs-marked-risky-by-AzureAD-IdentityProtection), um plug-in de exemplo que aproveita o nível de risco do usuário determinado pelo Azure ad Identity Protection para bloquear a autenticação ou impor a MFA (autenticação multifator). As etapas para criar um plug-in de usuário arriscado estão disponíveis [aqui](https://github.com/microsoft/adfs-sample-block-user-on-adfs-marked-risky-by-AzureAD-IdentityProtection)

## <a name="building-a-sample-plug-in"></a>Criando um plug-in de exemplo

>[!NOTE]
>Este passo a passos é apenas para mostrar como você pode criar um plug-in de exemplo. No entanto, não é a solução que estamos criando uma solução pronta para a empresa.

### <a name="pre-requisites"></a>Pré-requisitos
A seguir está a lista de pré-requisitos necessários para criar este plug-in de exemplo

- AD FS 2019 instalado e configurado
- .NET Framework 4,7 e superior
- Visual Studio

### <a name="build-plug-in-dll"></a>Criar dll de plug-in
O procedimento a seguir irá orientá-lo na criação de uma DLL de plug-in de exemplo.

1. Baixe o plug-in de exemplo, use o Git bash e digite o seguinte:

   ```
   git clone https://github.com/Microsoft/adfs-sample-RiskAssessmentModel-RiskyIPBlock
   ```

2. Crie um arquivo **. csv** em qualquer local no seu servidor de AD FS (no meu caso, criei o arquivo de **authconfigdb.csv** em **C:\Extensions**) e adicione os IPs que você deseja bloquear a esse arquivo.

   O plug-in de exemplo bloqueará as solicitações de autenticação provenientes dos **IPS de extranet** listados neste arquivo.

   >{! Observação] se você tiver um farm de AD FS, poderá criar o arquivo em qualquer ou em todos os servidores de AD FS. Qualquer um dos arquivos pode ser usado para importar os IPs arriscados para o AD FS. Discutiremos o processo de importação em detalhes na seção [registrar a DLL de plug-in com AD FS](#register-the-plug-in-dll-with-ad-fs) abaixo.

3. Abrir o projeto `ThreatDetectionModule.sln` usando o Visual Studio

4. Remova o `Microsoft.IdentityServer.dll` do Gerenciador de soluções, conforme mostrado abaixo:</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk2.png)

5. Adicione referência ao `Microsoft.IdentityServer.dll` de seu AD FS conforme mostrado abaixo

   a.    Clique com o botão direito do mouse em **referências** no **Gerenciador de soluções** e selecione **Adicionar referência...**</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk3.png)

   b.    Na janela **Gerenciador de referências** , selecione **procurar**. No **selecionar os arquivos a serem referenciados...** , selecione na `Microsoft.IdentityServer.dll` pasta de instalação do AD FS (no meu caso **C:\Windows\ADFS**) e clique em **Adicionar**.

   >[!NOTE]
   >No meu caso, estou criando o plug-in no próprio servidor de AD FS. Se o ambiente de desenvolvimento estiver em um servidor diferente, copie o `Microsoft.IdentityServer.dll` de sua pasta de instalação do AD FS no servidor AD FS na sua caixa de desenvolvimento.</br>

   ![modelo](media/ad-fs-risk-assessment-model/risk4.png)

   c.    Clique em **OK** na janela **Gerenciador de referências** depois de verificar se a caixa de `Microsoft.IdentityServer.dll` seleção está selecionada</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk5.png)

6. Todas as classes e referências estão agora em vigor para fazer uma compilação.   No entanto, como a saída desse projeto é uma dll, ele precisará ser instalado no **cache de assembly global**, ou GAC, do AD FS Server e a DLL precisa ser assinada primeiro. Isso pode ser feito da seguinte maneira:

   a.    **Clique com o botão direito do mouse** no nome do projeto, ThreatDetectionModule. No menu, clique em **Propriedades**.</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk6.png)

   b.    Na página **Propriedades** , clique em **assinatura**, à esquerda e marque a caixa de seleção **assinar o assembly**. No menu **escolher um arquivo de chave de nome forte**: suspenso, selecione **<novo... >**</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk7.png)

   c.    Na **caixa de diálogo Criar chave de nome forte**, digite um nome (você pode escolher qualquer nome) para a chave, desmarque a caixa de seleção **proteger meu arquivo de chave com senha**. Depois, clique em **OK**.</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk8.png)

   d.    Salve o projeto, conforme mostrado abaixo</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk9.png)

7. Crie o projeto clicando em **Compilar** e **Recompilar solução** , conforme mostrado abaixo</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk10.png)

   Verifique a **janela de saída**, na parte inferior da tela, para ver se ocorreram erros</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk11.png)


O plug-in (DLL) agora está pronto para uso e está na pasta **\bin\Debug** da pasta do projeto (no meu caso, isso é **C:\extensions\ThreatDetectionModule\bin\Debug\ThreatDetectionModule.dll**).

A próxima etapa é registrar essa DLL com AD FS, portanto, ela é executada em linha com AD FS processo de autenticação.

### <a name="register-the-plug-in-dll-with-ad-fs"></a>Registrar a DLL de plug-in com AD FS

Precisamos registrar a dll no AD FS usando o `Register-AdfsThreatDetectionModule` comando do PowerShell no servidor AD FS, no entanto, antes de registrarmos, precisamos obter o token de chave pública. Esse token de chave pública foi criado quando criamos a chave e assinamos a DLL usando essa chave. Para saber qual é o token de chave pública para a dll, você pode usar o **SN.exe** da seguinte maneira

1. Copie o arquivo dll da pasta **\bin\Debug** para outro local (em meu caso, copiando-o para **C:\Extensions**)

2. Inicie o **prompt de comando do desenvolvedor** para o Visual Studio e vá para o diretório que contém o **sn.exe** (no meu caso, o diretório é **c:\Arquivos de programas (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**) ![ modelo](media/ad-fs-risk-assessment-model/risk12.png)

3. Executar o comando **SN** com o parâmetro **-T** e o local do arquivo (no meu caso `SN -T "C:\extensions\ThreatDetectionModule.dll"` ) ![ modelo](media/ad-fs-risk-assessment-model/risk13.png)</br>
   O comando fornecerá o token de chave pública (para mim, o **token de chave pública é 714697626ef96b35**)

4. Adicione a dll ao **cache de assembly global** do AD FS Server. nossa prática recomendada seria criar um instalador adequado para seu projeto e usar o instalador para adicionar o arquivo ao GAC. Outra solução é usar **Gacutil.exe** (mais informações sobre **Gacutil.exe** disponíveis [aqui](/dotnet/framework/tools/gacutil-exe-gac-tool)) em seu computador de desenvolvimento.  Como tenho o Visual Studio no mesmo servidor que AD FS, usarei **Gacutil.exe** da seguinte maneira

   a.    No Prompt de Comando do Desenvolvedor para Visual Studio e vá para o diretório que contém o **Gacutil.exe** (no meu caso, o diretório é **C:\Program Files (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**)

   b.    Executar o modelo do comando **Gacutil** (no meu caso `Gacutil /IF C:\extensions\ThreatDetectionModule.dll` ) ![](media/ad-fs-risk-assessment-model/risk14.png)

   >[!NOTE]
   >Se você tiver um farm de AD FS, o acima precisará ser executado em cada servidor AD FS no farm.

5. Abra o **Windows PowerShell** e execute o comando a seguir para registrar a dll
   ```
   Register-AdfsThreatDetectionModule -Name "<Add a name>" -TypeName "<class name that implements interface>, <dll name>, Version=10.0.0.0, Culture=neutral, PublicKeyToken=< Add the Public Key Token from Step 2. above>" -ConfigurationFilePath "<path of the .csv file>"
   ```
   No meu caso, o comando é:
   ```
   Register-AdfsThreatDetectionModule -Name "IPBlockPlugin" -TypeName "ThreatDetectionModule.UserRiskAnalyzer, ThreatDetectionModule, Version=10.0.0.0, Culture=neutral, PublicKeyToken=714697626ef96b35" -ConfigurationFilePath "C:\extensions\authconfigdb.csv"
   ```

   >[!NOTE]
   >Você precisa registrar a DLL apenas uma vez, mesmo se tiver um farm de AD FS.

6. Reiniciar o serviço de AD FS depois de registrar a dll

É isso, a dll agora está registrada com AD FS e pronta para uso!

 >[!NOTE]
 > Se forem feitas alterações no plug-in e o projeto for recriado, a dll atualizada precisará ser registrada novamente. Antes de se registrar, será necessário cancelar o registro da dll atual usando o seguinte comando:</br></br>
 >`
  UnRegister-AdfsThreatDetectionModule -Name "<name used while registering the dll in 5. above>"
 >`</br></br>
 >No meu caso, o comando é:
 >```
 >UnRegister-AdfsThreatDetectionModule -Name "IPBlockPlugin"
 >```

### <a name="testing-the-plug-in"></a>Testando o plug-in

1. Abra o arquivo de **authconfig.csv** que criamos anteriormente (no meu caso no local **C:\Extensions**) e adicione os **IPS de extranet** que você deseja bloquear. Cada IP deve estar em uma linha separada e não deve haver espaços no final</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk18.png)

2. Salvar e fechar o arquivo

3. Importe o arquivo atualizado em AD FS executando o seguinte comando do PowerShell

   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "<name given while registering the dll>" -ConfigurationFilePath "<path of the .csv file>"
   ```

   No meu caso, o comando é:
   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "IPBlockPlugin" -ConfigurationFilePath "C:\extensions\authconfigdb.csv")
   ```

4. Inicie a solicitação de autenticação do servidor com o mesmo IP que você adicionou no **authconfig.csv**.

   Para esta demonstração, usarei [AD FS ferramenta ajuda de declarações X-Ray](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) para iniciar uma solicitação. Se você quiser usar a ferramenta X-Ray, siga as instruções

   Insira a instância do servidor de Federação e clique no botão de **autenticação de teste** .</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk15.png)

5. A autenticação é bloqueada conforme mostrado abaixo.</br>
   ![modelo](media/ad-fs-risk-assessment-model/risk16.png)

Agora que sabemos como criar e registrar o plug-in, vamos analisar o código do plug-in para entender a implementação usando as novas interfaces e classes introduzidas com o modelo.

## <a name="plug-in-code-walkthrough"></a>Instruções de código de plug-in

Abra o projeto `ThreatDetectionModule.sln` usando o Visual Studio e, em seguida, abra o arquivo principal **UserRiskAnalyzer.cs** no **Gerenciador de soluções** à direita da tela</br>
![modelo](media/ad-fs-risk-assessment-model/risk17.png)

O arquivo contém a classe principal UserRiskAnalyzer que implementa a classe abstrata [ThreatDetectionModule](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule) e a interface [IRequestReceivedThreatDetectionModule](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule) para ler o IP do contexto da solicitação, comparar o IP obtido com os IPs carregados do AD FS DB e bloquear a solicitação se houver uma correspondência de IP. Vamos examinar esses tipos mais detalhadamente

### <a name="threatdetectionmodule-abstract-class"></a>Classe abstrata ThreatDetectionModule

Essa classe abstrata carrega o plug-in no pipeline AD FS, possibilitando a execução do código de plug-in em linha com AD FS processo.

```
public abstract class ThreatDetectionModule
{
    protected ThreatDetectionModule();

    public abstract string VendorName { get; }
    public abstract string ModuleIdentifier { get; }

 public abstract void OnAuthenticationPipelineLoad(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData);
 public abstract void OnAuthenticationPipelineUnload(ThreatDetectionLogger logger);
  public abstract void OnConfigurationUpdate(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData);
 }
```
A classe inclui métodos e propriedades a seguir.

|Método |Type|Definição|
|-----|-----|-----|
|[OnAuthenticationPipelineLoad](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload) |Void|Chamado por AD FS quando o plug-in é carregado em seu pipeline|
|[OnAuthenticationPipelineUnload](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineunload) |Void|Chamado por AD FS quando o plug-in é descarregado de seu pipeline|
|[OnConfigurationUpdate](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate)| Void|Chamado por AD FS na atualização de configuração |
|**Propriedade** |**Tipo** |**Definição**|
|[Nome_do_Fornecedor](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.vendorname)|String |Obtém o nome do fornecedor que possui o plug-in|
|[ModuleIdentifier](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.moduleidentifier)|String |Obtém o identificador do plug-in|

Em nosso plug-in de exemplo, estamos usando os métodos [OnAuthenticationPipelineLoad](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload) e [OnConfigurationUpdate](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate) para ler os IPs predefinidos do AD FS DB. [OnAuthenticationPipelineLoad](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload) é chamado quando o plug-in é registrado com AD FS enquanto [OnConfigurationUpdate](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate) é chamado quando o. csv é importado usando o `Import-AdfsThreatDetectionModuleConfiguration` cmdlet.

#### <a name="irequestreceivedthreatdetectionmodule-interface"></a>Interface IRequestReceivedThreatDetectionModule

Essa [interface](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule) permite que você implemente a avaliação de riscos no ponto em que AD FS recebe a solicitação de autenticação, mas antes que o usuário insira as credenciais, ou seja, no estágio de solicitação recebida do processo de autenticação.

```
public interface IRequestReceivedThreatDetectionModule
{
Task<ThrottleStatus> EvaluateRequest (
ThreatDetectionLogger logger,
RequestContext requestContext );
}
```

A interface inclui o método [EvaluateRequest](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest) , que permite que você use o contexto da solicitação de autenticação passada no parâmetro de entrada RequestContext para escrever a lógica de avaliação de riscos. O parâmetro requestContext é do tipo [RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext).

O outro parâmetro de entrada passado é Logger, que é do tipo [ThreatDetectionLogger](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger). O parâmetro pode ser usado para gravar o erro, auditar e/ou depurar mensagens para AD FS logs.

O método retorna [ThrottleStatus](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus) (0 se não avaliado, 1 para bloquear e 2 para permitir) para AD FS que, em seguida, bloqueia ou permite a solicitação.

Em nosso plug-in de exemplo, a implementação do método [EvaluateRequest](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest) analisa o [ClientIpAddress](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext.clientipaddresses#Microsoft_IdentityServer_Public_ThreatDetectionFramework_RequestContext_ClientIpAddresses) do parâmetro [RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext) e o compara com todos os IPs carregados do AD FS DB. Se uma correspondência for encontrada, o método retornará 2 para **bloco**, caso contrário retornará 1 para **permitir**. Com base no valor retornado, o AD FS bloqueia ou permite a solicitação.

>[!NOTE]
>O plug-in de exemplo discutido acima implementa somente a interface IRequestReceivedThreatDetectionModule. No entanto, o modelo de avaliação de risco fornece duas interfaces adicionais – IPreAuthenticationThreatDetectionModule (para implementar a fase de pré-autenticação durante lógica de avaliação de risco) e IPostAuthenticationThreatDetectionModule (para implementar a lógica de avaliação de risco durante o estágio pós-autenticação). Os detalhes sobre as duas interfaces são fornecidos abaixo.

#### <a name="ipreauthenticationthreatdetectionmodule-interface"></a>Interface IPreAuthenticationThreatDetectionModule

Essa [interface](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule) permite que você implemente a lógica de avaliação de riscos no ponto em que o usuário fornece as credenciais, mas antes que AD FS as avalie, ou seja, o estágio de pré-autenticação.

```
public interface IPreAuthenticationThreatDetectionModule
{
Task<ThrottleStatus> EvaluatePreAuthentication (
ThreatDetectionLogger logger,
RequestContext requestContext,
SecurityContext securityContext,
ProtocolContext protocolContext,
IList<Claim> additionalClams
);
}
```
A interface inclui o método [EvaluatePreAuthentication](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule.evaluatepreauthentication) , que permite que você use as informações passadas nos parâmetros de entrada [RequestContext RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext), [SecurityContext SecurityContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext), [ProtocolContext ProtocolContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext)e [IList <Claim> additionalClams](/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) para gravar a lógica de avaliação de risco de pré-autenticação.

>[!NOTE]
>Para obter a lista de propriedades passadas com cada tipo de contexto, visite as definições de classe [RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext), [SecurityContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext)e [ProtocolContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext) .

O outro parâmetro de entrada passado é Logger, que é do tipo [ThreatDetectionLogger](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger). O parâmetro pode ser usado para gravar o erro, auditar e/ou depurar mensagens para AD FS logs.

O método retorna [ThrottleStatus](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus) (0 se não avaliado, 1 para bloquear e 2 para permitir) para AD FS que, em seguida, bloqueia ou permite a solicitação.

#### <a name="ipostauthenticationthreatdetectionmodule-interface"></a>Interface IPostAuthenticationThreatDetectionModule

Essa [interface](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule) permite que você implemente a lógica de avaliação de riscos após o usuário fornecer credenciais e AD FS realizou a autenticação, ou seja, o estágio pós-autenticação.

```
public interface IPostAuthenticationThreatDetectionModule
{
Task<RiskScore> EvaluatePostAuthentication (
ThreatDetectionLogger logger,
RequestContext requestContext,
SecurityContext securityContext,
ProtocolContext protocolContext,
AuthenticationResult authenticationResult,
IList<Claim> additionalClams
);
}
```

A interface inclui o método [EvaluatePostAuthentication](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule.evaluatepostauthentication) , que permite que você use as informações passadas nos parâmetros de entrada [RequestContext RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext), [SecurityContext SecurityContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext), [ProtocolContext ProtocolContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext)e [IList <Claim> additionalClams](/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) para gravar a lógica de avaliação de risco pós-autenticação.

>[!NOTE]
> Para obter uma lista completa das propriedades passadas com cada tipo de contexto, consulte definições de classe [RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext), [SecurityContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext)e [ProtocolContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext) .

O outro parâmetro de entrada passado é Logger, que é do tipo [ThreatDetectionLogger](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger). O parâmetro pode ser usado para gravar o erro, auditar e/ou depurar mensagens para AD FS logs.

O método retorna a [Pontuação de risco](/dotnet/api/microsoft.identityserver.authentication.riskscoreconstants) que pode ser usada na política de AD FS e em regras de declaração.

>[!NOTE]
>Para que o plug-in funcione, a classe principal (nesse caso, UserRiskAnalyzer) precisa derivar a classe abstrata [ThreatDetectionModule](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule) e deve implementar pelo menos uma das três interfaces descritas acima. Depois que a dll é registrada, o AD FS verifica quais das interfaces são implementadas e as chama no estágio apropriado no pipeline.

### <a name="faqs"></a>Perguntas frequentes

**Por que devo criar esses plug-ins?**</br>
**R:** Esses plug-ins não só fornecem recursos adicionais para proteger seu ambiente contra ataques como ataques de irrigação de senha, mas também oferecem a flexibilidade para criar sua própria lógica de avaliação de riscos com base em suas necessidades.

**Onde os logs são capturados?**</br>
**R:** Você pode gravar logs de erros no log de eventos "AD FS/admin" usando o método WriteAdminLogErrorMessage, logs de auditoria no log de segurança de "AD FS auditoria" usando o método WriteAuditMessage e logs de depuração para o log de depuração "AD FS rastreamento" usando o método WriteDebugMessage.

**O pode adicionar esses plug-ins aumentar AD FS latência de processo de autenticação?**</br>
**R:** O impacto de latência será determinado pelo tempo necessário para executar a lógica de avaliação de risco que você implementar. É recomendável avaliar o impacto de latência antes de implantar o plug-in no ambiente de produção.

**Por que não é possível AD FS sugerir a lista de IPs arriscados, usuários, etc.?**</br>
**R:** Embora não esteja disponível no momento, estamos trabalhando na criação da inteligência para sugerir IPs arriscados, usuários, etc. no modelo de avaliação de risco conectável. Compartilharemos as datas de lançamento em breve.

**Quais outros plug-ins de exemplo estão disponíveis?**</br>
**R:** Os seguintes plug-ins de exemplo estão disponíveis:

|Nome|Descrição|
|-----|-----|
|[Plug-in de usuário arriscado](https://github.com/microsoft/adfs-sample-block-user-on-adfs-marked-risky-by-AzureAD-IdentityProtection)|Plug-in de exemplo que bloqueia a autenticação ou impõe a MFA com base no nível de risco do usuário determinado por Azure AD Identity Protection.|
