---
title: Ajustar a compactação do grupo de disponibilidade | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 7632769c-b246-4766-886f-7c60ec540be8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3891d30ef5bfffb19ca1d4bfcaab290e3903816b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013669"
---
# <a name="tune-compression-for-availability-group"></a>Ajustar a compactação do grupo de disponibilidade
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Por padrão, o SQL Server compacta fluxos de dados, quando apropriado, de grupos de disponibilidade. A compactação reduz o tráfego de rede, aumenta a carga da CPU e pode induzir a latência. Você deve ser membro da função de servidor fixa sysadmin para habilitar a compactação. A seguinte tabela mostra os casos em que o SQL Server usa a compactação para os fluxos de log do grupo de disponibilidade:

| Cenário | Configuração da compactação
| ---- | ----
| Réplica de confirmação síncrona | Não compactado
| Réplicas de confirmação assíncrona | Compressed
| Durante a propagação automática | Não compactado

## <a name="trace-flags-for-availability-group-compression"></a>Sinalizadores de rastreamento para a compactação do grupo de disponibilidade 

Na maioria dos cenários, a Microsoft não recomenda alterar essas configurações. É possível usar sinalizadores de rastreamento global para testar a alteração dessas configurações. O SQL Server aplica os sinalizadores de rastreamento global a toda a instância. Todos os grupos de disponibilidade na instância serão afetados por essas configurações.  

A tabela a seguir mostra os sinalizadores de rastreamento que alterarão o comportamento padrão da compactação do SQL Server. 

Sinalizador de rastreamento | Descrição
------------- | -------------
1462          | Desabilita a compactação do fluxo de logs dos Grupos de Disponibilidade com réplicas síncronas. Esse recurso está habilitado por padrão em réplicas assíncronas para otimizar a largura de banda de rede.
9567          | Habilita a compactação do fluxo de dados em Grupos de Disponibilidade durante a propagação automática. Durante a propagação automática, a compactação pode reduzir de forma significativa o tempo de transferência e aumentará a carga no processador.
9592          | Habilita a compactação do fluxo de logs dos Grupos de Disponibilidade com réplicas síncronas. Esse recurso está desabilitado por padrão em réplicas síncronas, pois a compactação adiciona latência. A compactação do fluxo de log está habilitada por padrão em réplicas assíncronas.


## <a name="resources"></a>Recursos


[Opções de inicialização do Mecanismo de Banco de Dados](../../../database-engine/configure-windows/database-engine-service-startup-options.md)

[Propagação automática](https://msdn.microsoft.com/library/mt735149(SQL.130).aspx)

[Pré-requisitos do AlwaysOn](prereqs-restrictions-recommendations-always-on-availability.md) 
