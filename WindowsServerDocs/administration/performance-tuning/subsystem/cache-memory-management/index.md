---
title: Ajuste de desempenho para subsistemas de gerenciador de memória e cache
description: Ajuste de desempenho para subsistemas de gerenciador de memória e cache
ms.topic: landing-page
ms.author: pavel
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 8c5800dc0f4d55d7cb240496a304dd56b97077f1
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078013"
---
# <a name="performance-tuning-cache-and-memory-manager"></a>Ajuste de desempenho para gerenciador de memória e cache

Por padrão, o Windows armazena em cache os dados de arquivo que são lidos em discos e gravados em discos. Isso significa que as operações de leitura leem dados de arquivos de uma área na memória do sistema conhecida como o cache de arquivo do sistema, em vez do disco físico. Do mesmo modo, as operações de gravação gravam dados de arquivo no cache de arquivo do sistema em vez de no disco, e esse tipo de cache é conhecido como um cache de write-back. O armazenamento em cache é gerenciado por um objeto de arquivo. O armazenamento em cache ocorre sob a direção do Gerenciador de Cache, que opera continuamente durante a execução do Windows.

Os dados de arquivo no cache do sistema de arquivos são gravados no disco em intervalos determinados pelo sistema operacional. As páginas liberadas permanecem no conjunto de trabalho do cache do sistema (quando FILE\_FLAG\_RANDOM\_ACCESS for definido e o identificador de arquivo não estiver fechado) ou na lista de espera na qual elas se tornam parte da memória disponível.

A política de atrasar a gravação dos dados no arquivo e mantê-los no cache até que o cache seja liberado é chamada de gravação lenta, e é acionada pelo Gerenciador de Cache em um intervalo de tempo determinado. A hora na qual um bloco de dados de arquivo é liberado tem base em parte na quantidade de tempo que ele ficou armazenado no cache e na quantidade de tempo desde que os dados foram acessados pela última vez em uma operação de leitura. Isso garante que os dados de arquivos lidos com frequência permaneçam acessíveis no cache de arquivo do sistema pelo máximo de tempo.

Esse processo de armazenamento em cache de dados do arquivo é ilustrado na figura a seguir:

![armazenamento em cache de dados do arquivo](../../media/perftune-guide-file-data-caching.png)

Conforme representado pelas setas sólidas na figura anterior, uma região com 256 KB de dados é lida em um slot de cache de 256 KB no espaço de endereço do sistema na primeira solicitação pelo Gerenciador de Cache durante uma operação de leitura de arquivo. Em seguida, um processo do modo de usuário copia os dados deste slot em seu próprio espaço de endereço. Após a conclusão do acesso a dados pelo processo, ele grava os dados alterados de volta ao mesmo slot no cache do sistema, como mostrado a seta pontilhada entre o espaço de endereço do processo e o cache do sistema. Quando o Gerenciador de Cache determinar que os dados não são mais necessários para um determinado período, ele gravará os dados alterados novamente no arquivo no disco, conforme mostra a seta pontilhada entre o cache do sistema e o disco.

**Nesta seção:**

-   [Possíveis problemas de desempenho do Gerenciador de Memória e do Cache](troubleshoot.md)

-   [Aprimoramentos de cache e Gerenciador de Memória no Windows Server 2016](./improvements-in-windows-server.md)