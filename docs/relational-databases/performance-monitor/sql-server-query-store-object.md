---
title: SQL Server, objeto Repositório de consulta | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: aba8942612be6c7b33883bb109146170583b5b95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62649413"
---
# <a name="sql-server-query-store-object"></a>SQL Server, Objeto de Repositório de Consultas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O objeto de Repositório de Consultas fornece contadores para monitorar a utilização de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar textos de consulta, planos de execução e estatísticas de tempo de execução para objetos, como procedimentos armazenados, instruções ad hoc e preparadas do [!INCLUDE[tsql](../../includes/tsql-md.md)] e gatilhos.  
  
 Esta tabela descreve os contadores do **SQLServer:Repositório de Consultas**.  
  
|Contadores de Repositório de Consultas do SQL Server|Descrição|  
|-------------------------------------|-----------------|  
|**Uso de CPU do Repositório de Consultas**|Indica o uso da CPU pelos Repositórios de Consultas.|  
|**Leituras lógicas do Repositório de Consultas**|Indica o número de leituras lógicas feitas pelo Repositório de Consultas.|  
|**Gravações lógicas do Repositório de Consultas**|Indica a quantidade de dados que estão sendo enfileirados para liberação a partir do Repositório de Consultas. A frequência e o atraso na adição de itens (que representam as estatísticas de tempo de execução) para a fila são controlados pela configuração do Intervalo de Liberação de Dados.|  
|**Leituras físicas do Repositório de Consultas**|Indica o número de leituras físicas feitas pelo Repositório de Consultas.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Instância do Repositório de Consultas|Descrição|  
|--------------------------|-----------------|  
|**_Total**|Informações para o Repositório de Consultas para esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|\<nome do banco de dados>|Informações do Repositório de Consultas para este banco de dados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
