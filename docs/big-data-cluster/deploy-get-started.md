---
title: Introdução
titleSuffix: SQL Server big data clusters
description: Aprenda as etapas e os recursos de implantação de clusters de big data de 2019 do SQL Server (visualização).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8583610606e5d554f039a69688af3ddff8dc8bb3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958538"
---
# <a name="get-started-with-sql-server-big-data-clusters"></a>Introdução aos clusters de grandes dados do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece uma visão geral de como implantar um [cluster de big data (visualização) do SQL Server 2019](big-data-cluster-overview.md). Ele destina-se para orientar você aos conceitos e fornecer uma estrutura de Noções básicas sobre os outros artigos nesta seção implantação. As etapas de implantação específico variam com base em suas opções de plataforma para o cliente e servidor.

## <a id="tools"></a> Ferramentas de cliente

Os clusters de big data exigem um conjunto de ferramentas de cliente específico. Antes de implantar um cluster de big data no Kubernetes, você deve instalar as ferramentas a seguir:

| Ferramenta | Descrição |
|---|---|
| **mssqlctl** | Implanta e gerencia clusters de big data. |
| **kubectl** | Cria e gerencia o cluster Kubernetes subjacente. |
| **Azure Data Studio** | Interface gráfica para usar o cluster de big data. |
| **Extensão do SQL Server de 2019** | Extensão de dados Studio do Azure que habilita os recursos de cluster de big data. |

Outras ferramentas são necessárias para cenários diferentes. Cada artigo deve explicar as ferramentas de pré-requisitos para executar uma tarefa específica. Para obter uma lista completa de ferramentas e links de instalação, consulte [ferramentas de big data de instalar o SQL Server 2019](deploy-big-data-tools.md).

## <a name="kubernetes"></a>Kubernetes

Clusters de big data são implantados como uma série de inter-relacionados contêineres que são gerenciados no [Kubernetes](https://kubernetes.io/docs/home). Você pode hospedar Kubernetes em uma variedade de formas. Mesmo se você já tiver um ambiente existente do Kubernetes, você deve revisar os requisitos relacionados para clusters de big data.

- **Serviço de Kubernetes do Azure (AKS)** : AKS permite que você implante um cluster Kubernetes gerenciado no Azure. Somente você gerencia e manter os nós de agente. Com o AKS, você não precisa provisionar seu próprio hardware para o cluster. Também é fácil de usar um cluster de big data [script de implantação](quickstart-big-data-cluster-deploy.md) para criar o cluster do AKS e implantar o cluster de big data em uma única etapa. Para obter mais informações sobre como usar o AKS com clusters de big data, consulte [configurar o serviço de Kubernetes do Azure para implantações de cluster (versão prévia) do SQL Server 2019 big data](deploy-on-aks.md).

- **Várias máquinas**: Você também pode implantar Kubernetes em várias máquinas Linux, o que poderia ser servidores físicos ou máquinas virtuais. O [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) ferramenta pode ser usada para criar o cluster Kubernetes. Esse método funciona bem se você já tiver uma infraestrutura existente que você deseja usar para seu cluster de big data. Para obter mais informações sobre como usar **kubeadm** implantações com clusters de big data, consulte [configurar Kubernetes em vários computadores para implantações de cluster (versão prévia) do SQL Server 2019 big data](deploy-with-kubeadm.md).

- **Minikube**: Minikube permite que você executar o Kubernetes localmente em um único servidor. É uma boa opção se você estiver experimentando a clusters de dados grande ou precisar usá-lo em um cenário de teste ou desenvolvimento. Para obter mais informações sobre como usar o Minikube, consulte o [Minikube documentação](https://kubernetes.io/docs/setup/minikube/). Para obter requisitos específicos para usar o Minikube com clusters de big data, consulte [configurar o minikube para implantações de cluster de big data do SQL Server 2019](deploy-on-minikube.md).

## <a name="deploy-a-big-data-cluster"></a>Implantar um cluster de Big Data

Depois de configurar o Kubernetes, você implanta um cluster de big data com o `mssqlctl bdc create` comando. Durante a implantação, você pode aproveitar as várias abordagens diferentes.

- Se você estiver implantando em um ambiente de desenvolvimento e teste, você pode optar por usar um dos [as configurações padrão](deployment-guidance.md#deploy) fornecidas pelo **mssqlctl**.

- Para personalizar sua implantação, você pode criar e usar seu próprio [arquivos de configuração de implantação](deployment-guidance.md#configfile).

- Para uma instalação totalmente autônoma, você pode passar todas as outras configurações em variáveis de ambiente. Para obter mais informações, consulte [implantações autônomas](deployment-guidance.md#unattended).

## <a name="deployment-scripts"></a>Scripts de implantação

Scripts de implantação podem ajudar a implantar Kubernetes e clusters de big data em uma única etapa. Eles também costumam ser fornecerem valores padrão para as configurações de cluster de big data. Para obter um exemplo de um script de implantação de cluster de big data no serviço de Kubernetes do Azure (AKS), consulte o artigo a seguir:

[Implantar um servidor de SQL 2019 grandes dados de cluster com um script de implantação (AKS)](quickstart-big-data-cluster-deploy.md).

Você pode personalizar qualquer script de implantação ao criar sua própria versão que configura as variáveis de ambiente de cluster de big data de forma diferente.

## <a name="next-steps"></a>Próximas etapas

Depois de implantar um cluster de big data com êxito [conectar-se ao cluster](connect-to-big-data-cluster.md) e considere [carregar dados de exemplo](tutorial-load-sample-data.md) para uso com várias instruções passo a passo.