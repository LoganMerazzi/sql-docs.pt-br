---
title: Usando o SQL Server Profiler para monitorar a mineração de dados | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ba9720f87cd41849cc118482ffbf4731049e8c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209551"
---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>Usando o SQL Server Profiler para monitorar a mineração de dados (Analysis Services - Mineração de dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se tiver as permissões necessárias, você poderá usar o SQL Server Profiler para monitorar as atividades de mineração de dados emitidas como solicitações enviadas a uma instância do SQL Server Analysis Services. A atividade de mineração de dados pode incluir o processamento de modelos ou estruturas, consultas de previsão ou consultas de conteúdo ou a criação de novos modelos ou estruturas.  
  
 O SQL Server Profiler usa um **rastreamento** para monitorar as solicitações enviadas de vários clientes, incluindo o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o SQL Server Management Studio, serviços Web ou Suplementos de Mineração de Dados para o Excel, contanto que todas as atividades usem a mesma instância do SQL Server Analysis Services. Você deve criar um rastreamento separado para cada instância do SQL Server Analysis Services que deseja monitorar. Para obter informações gerais sobre rastreamentos e como usar o SQL Server Profiler, consulte [Usar o SQL Server Profiler para monitorar o Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Para obter orientações específicas sobre os tipos de eventos capturados, consulte [Criar rastreamentos do Profiler para reprodução &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md).  
  
## <a name="using-traces-to-monitor-data-mining"></a>Usando rastreamentos para monitorar a mineração de dados  
 Ao capturar informações em um rastreamento, você pode especificar se as informações estão salvas em um arquivo ou em uma tabela em uma instância do SQL Server. Independentemente do método usado para armazenar os dados, você pode usar o SQL Server Profiler para exibir o rastreamento e aplicar filtros por eventos. A tabela a seguir lista alguns eventos e subclasses do rastreamento padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que são de interesse para a mineração de dados.  
  
|EventClass|EventSubclass|Descrição|  
|----------------|-------------------|-----------------|  
|**Query Begin**<br /><br /> **Query End**|**0 - MDXQuery**|Contém o texto de todas as chamadas para os procedimentos armazenados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|**Query Begin**<br /><br /> **Query End**|**1 - DMXQuery**|Contém o texto e os resultados das instruções DMX.|  
|**Progress Report Begin**<br /><br /> **Progress Report End**|**34 - DataMiningProgress**|Fornece informações sobre o andamento do algoritmo de mineração de dados: por exemplo, se você estiver criando um modelo de clustering, a mensagem de andamento informará qual cluster candidato está sendo criado|  
|**Query Begin**<br /><br /> **Query End**|EXECUTESQL|Contém o texto da consulta Transact-SQL que está sendo executada|  
|**Query Begin**<br /><br /> **Query End**|**2- SQLQuery**|Contém o texto de todas as consultas dos conjuntos de linhas de esquema no formulário de tabelas do sistema.|  
|**Início de DISCOVER**<br /><br /> **Término de DISCOVER**|Vários|Contém o texto das chamadas de função DMX ou das instruções DISCOVER, encapsuladas em XMLA.|  
|**Erro**|(nenhum)|Contém o texto de erros enviados pelo servidor ao cliente.<br /><br /> Mensagens de erro que começam com **Erro (Mineração de Dados):** ou **Informativo (Mineração de Dados):** são geradas especificamente em resposta a solicitações DMX. Porém, não é suficiente exibir só estas mensagens de erro. Outros erros, como os gerados pelo analisador, podem estar relacionados à mineração de dados, mas não ter este prefixo.|  
  
 Exibindo as instruções de comando no log de rastreamento, você também pode ver a sintaxe de instruções complexas enviadas pelo cliente ao servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , incluindo as chamadas aos procedimentos armazenados do sistema. Essas informações podem ser úteis para depuração ou você pode usar instruções válidas como um modelo para criar novos modelos ou consultas de previsão. Para obter alguns exemplos de chamadas de procedimento armazenado que podem ser capturadas por um rastreamento, consulte [Exemplos de consulta de modelo de clustering](../../analysis-services/data-mining/clustering-model-query-examples.md).  
  
## <a name="see-also"></a>Consulte também  

 [Monitorar o Analysis Services com Eventos Estendidos do SQL Server](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  
