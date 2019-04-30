---
title: Configurar o minikube
titleSuffix: SQL Server big data clusters
description: Saiba como configurar o minikube para implantações de cluster (versão prévia) do SQL Server 2019 big data em um único computador.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: afa5c3bae6eb7898ccaedf534382c9aeb467f01c
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473500"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>Configurar o minikube para implantações de cluster de big data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como configurar **minikube** em um único computador para implantações de cluster (versão prévia) do SQL Server 2019 big data. Minikube é uma ferramenta que torna mais fácil de executar Kubernetes em um único computador, como um laptop ou desktop. Minikube executa um cluster do Kubernetes de nó único dentro de uma VM em seu laptop para usuários que desejam experimentar Kubernetes ou desenvolver com ele diárias. 

## <a name="prerequisites"></a>Prerequisites

- 32 GB de memória (64 GB recomendado).

- Se o computador tem apenas o mínimo recomendado de memória, em seguida, configure a implantação do cluster para ter apenas 1 instância de pool de computação, 1 instância de pool de dados e instância de pool de armazenamento de 1. Essa configuração só deve ser usada para ambientes de avaliação em que a durabilidade e disponibilidade dos dados são importantes. Consulte a [documentação de implantação](deployment-guidance.md#configfile) para obter mais informações sobre as variáveis de ambiente para configurar o número de réplicas para pools de dados, computação pools e pools de armazenamento.

- Virtualização x VT ou AMD-v deve ser habilitada no BIOS do computador.

## <a name="install-dependencies"></a>Instale as dependências

1. Instale [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Instale o Python 3:
   - Se o pip está ausente, baixe [get-clspip.py](https://bootstrap.pypa.io/get-pip.py) e execute `python get-pip.py`.
   - Solicitações de instalação de pacote usando `python -m pip install requests`.

1. Se você ainda não tiver um hipervisor instalado, instale um agora.
   - Para OS X, instale [driver xhyve](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads), ou [VMware Fusion](https://www.vmware.com/products/fusion).
   - Para o Linux, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) ou [KVM](https://www.linux-kvm.org/).
   - Para Windows, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) ou [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Se você não tiver um comutador externo configurado no hyper-v, em seguida, crie um que tenha acesso à rede externa.  Veja como [criar um comutador externo no hyper-v para minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Instalar o minikube

Instalar o minikube de acordo com as instruções para o [v0.28.2 versão](https://github.com/kubernetes/minikube/releases/tag/v0.28.2). O cluster de big data de 2019 do SQL Server (versão prévia) funciona somente com a versão v0.24.1 e backup.

## <a name="create-a-minikube-cluster"></a>Criar um cluster do minikube

O comando a seguir cria um cluster do minikube em uma VM do Hyper-V com 8 CPUs, 28 GB de memória e o tamanho do disco de 100 GB. O tamanho do disco não é um espaço reservado.  Ele cresce para que o tamanho em disco conforme necessário.  É recomendável não alterar o disco de espaço para algo menos de 100 GB tivemos problemas com isso no teste. Isso também especifica o comutador do hyper-v com acesso externo explicitamente.

Alterar os parâmetros, como **– memória** conforme necessário, dependendo de seu hardware disponível e que hipervisor que você está usando.  Verifique se o **– hyper-v** valor do parâmetro de comutador virtual corresponde ao nome que você usou ao criar o comutador virtual.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

Se você estiver usando o minikube com o VirtualBox, o comando teria esta aparência:

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Desabilitar ponto de verificação automático com o Hyper-V

No Windows 10, o ponto de verificação automático está habilitado em uma máquina virtual. Execute o comando a seguir no PowerShell para desabilitar o ponto de verificação automático na VM.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>Próximas etapas

As etapas neste artigo configurado um cluster minikube. A próxima etapa é implantar um cluster de big data do SQL Server 2019. Para obter instruções, consulte o artigo a seguir:

[Implantar clusters de grandes dados do SQL Server 2019 no Kubernetes](deployment-guidance.md#deploy)
