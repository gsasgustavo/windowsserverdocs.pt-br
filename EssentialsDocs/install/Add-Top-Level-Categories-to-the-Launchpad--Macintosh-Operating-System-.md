---
title: Adicionar Categorias de Nível Superior à Barra Inicial (Sistema Operacional Macintosh)
description: Saiba como adicionar categorias de nível superior à Launchpad em um computador que executa o sistema operacional Macintosh.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: ee2173c3-e464-4001-9f43-6d926a575092
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 09cbae3e6643e9ebd729c06646647b361374c787
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711621"
---
# <a name="add-top-level-categories-to-the-launchpad-macintosh-operating-system"></a>Adicionar Categorias de Nível Superior à Barra Inicial (Sistema Operacional Macintosh)

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Você pode adicionar categorias de nível superior para a Barra Inicial em um computador executando o sistema operacional Macintosh. Para criar um suplemento de Launchpad que adiciona categorias de nível superior, você pode usar uma combinação de informações desta página e do tópico intitulado como: adicionar tarefas e categorias à Launchpad? no [SDK das soluções do Windows Server](https://go.microsoft.com/fwlink/?LinkID=248648).

 O seguinte exemplo mostra como você pode especificar para que a entrada da Barra Inicial seja uma categoria de nível superior no arquivo .launchpad:

```

<?xml version="1.0" encoding="utf-8" ?>
<LaunchPad resFile="Localizable">
   <Category id="Microsoft.Launchpad.HomeCategory" name="SampleAddin"  image="SampleImage01.png">
      <Task id="Microsoft.Launchpad.SampleAddin.Pictures"
          name="Pictures"
           src="smb://%ServerAddress%/Pictures"
         image="SampleImage02.png"/>
   </Category>
</LaunchPad>
```

 Para que a entrada seja uma categoria de nível superior, o atributo Id do elemento Category deve ser "Microsoft.Launchpad.HomeCategory".

## <a name="see-also"></a>Consulte Também
 [Criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para](Preparing-the-Image-for-Deployment.md) [testar a implantação da experiência do cliente](Testing-the-Customer-Experience.md)