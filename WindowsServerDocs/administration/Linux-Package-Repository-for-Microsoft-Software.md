---
title: Repositório de software do Linux para produtos da Microsoft
description: Este documento descreve como usar e instalar pacotes de software do Linux para produtos da Microsoft.
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: victorcheng7
ms.author: vichen
ms.date: 08/14/2020
ms.openlocfilehash: 28ce502a78c58eda74d5b412fe4e4d0d3279d442
ms.sourcegitcommit: dac52260fdcc3721daf7e32cd45760a0ced96de7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91663677"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Repositório de software do Linux para produtos da Microsoft

## <a name="overview"></a>Visão geral

A Microsoft cria e dá suporte a uma variedade de produtos de software para sistemas Linux e os torna disponíveis por meio dos repositórios de pacote APT e YUM padrão. Este documento descreve como configurar o repositório em seu sistema Linux, para que você possa instalar/atualizar o software Linux da Microsoft usando as ferramentas de gerenciamento de pacotes padrão de sua distribuição.

O repositório de software do Linux da Microsoft é composto por vários repositórios:

 - prod – o subrepositório de produção é designado para pacotes destinados para uso na produção. Esses pacotes têm suporte comercial da Microsoft sob os termos do contrato de suporte ou do programa aplicável que você tem com a Microsoft.

 - MSSQL-Server-esses repositórios contêm pacotes para Microsoft SQL Server em Linux-consulte também: [SQL Server em Linux](https://www.microsoft.com/sql-server/sql-server-vnext-including-Linux).

> [!NOTE]
> Os pacotes nos repositórios de software do Linux estão sujeitos aos termos de licença localizados nos pacotes. Leia os termos de licença antes de utilizar o pacote. A instalação e o uso do pacote constitui a aceitação desses termos. Se você não concorda com os termos de licença, não utilize o pacote.

## <a name="configuring-the-repositories"></a>Configurando os repositórios

Os repositórios podem ser configurados automaticamente instalando o pacote do Linux que se aplica à sua distribuição e versão do Linux. O pacote instalará a configuração do repositório junto com a chave pública GPG usada por ferramentas como apt/yum/zypper para validar os pacotes assinados e/ou os metadados do repositório.

### <a name="enterprise-linux-rhel-and-variants"></a>Linux corporativo (RHEL e variantes)

 - Enterprise Linux 6 (EL6)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm`

 - Enterprise Linux 7 (EL7)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm`

 - Enterprise Linux 8 (EL8)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/8/packages-microsoft-prod.rpm`

### <a name="suse"></a>SUSE

 - SUSE Linux Enterprise Server 12<p>`sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm`

 - SUSE Linux Enterprise Server 15<p>`sudo rpm -Uvh https://packages.microsoft.com/config/sles/15/packages-microsoft-prod.rpm`

### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 16, 4 (Xenial)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/16.04/prod`<p>`sudo apt-get update`

 - Ubuntu 18, 4 (Bionic)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod`<p>`sudo apt-get update`

 - Ubuntu 20, 4 (focal)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/20.04/prod`<p>`sudo apt-get update`

## <a name="manual-configuration"></a>Configuração manual

Os arquivos de configuração do repositório estão disponíveis em [Packages.Microsoft.com/config](https://packages.microsoft.com/config/). O nome e o local desses arquivos podem ser localizados usando a seguinte convenção de nomenclatura de URI:

`https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)`

### <a name="package-and-repository-signing-key"></a>Chave de assinatura de pacote e repositório

- A chave pública do GPG da Microsoft pode ser baixada aqui: [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
- ID da chave pública: Microsoft (assinatura de liberação) <gpgsecurity@microsoft.com>
- Impressão digital da chave pública: `BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>Exemplos

 - RHEL/CentOS 7

```
# Install repository configuration
curl -sSL https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft-prod.repo

# Install Microsoft's GPG public key
curl -sSL https://packages.microsoft.com/keys/microsoft.asc > ./microsoft.asc
sudo rpm --import ./microsoft.asc
```

 - Ubuntu 20.04

```
# Install repository configuration
curl -sSL https://packages.microsoft.com/config/ubuntu/20.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft-prod.list

# Install Microsoft GPG public key
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Update package index files
sudo apt-get update
```
