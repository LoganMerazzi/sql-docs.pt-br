---
title: Como o Repositório de Consultas coleta dados | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83fbc6c183216cedcbb664a0c3a2e3a9337e1513
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946778"
---
# <a name="how-query-store-collects-data"></a>Como o Repositório de Consultas coleta dados
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  O Repositório de Consultas funciona como um **gravador de dados de voo** constantemente coletando informações de compilação e tempo de execução relacionadas a consultas e planos. As consultas relacionadas a dados são mantidas em tabelas internas e apresentadas aos usuários por meio de um conjunto de exibições.  
  
## <a name="views"></a>Exibições  
 O diagrama a seguir mostra os modos de exibição do Repositório de Consultas e suas relações lógicas, com informações de tempo de compilação, apresentadas como entidades azuis:  
  
 ![query-store-process-2views](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**Descrições de exibições**  
  
|Exibição|Descrição|  
|----------|-----------------|  
|**sys.query_store_query_text**|Apresenta os textos de consulta exclusivos executados no banco de dados. Comentários e espaços antes e depois o texto da consulta são ignorados. Comentários e espaços dentro do texto não são ignorados. Cada instrução no lote gera uma entrada de texto de consulta separada.|  
|**sys.query_context_settings**|Apresenta as combinações exclusivas do plano que afetam as configurações em que as consultas são executadas. O mesmo texto de consulta executado com um plano diferente, afetando as configurações produz a entrada de consulta separada no Repositório de Consultas porque `context_settings_id` faz parte da chave de consulta.|  
|**sys.query_store_query**|Entradas de consulta que são controladas e forçadas separadamente no Repositório de Consultas. Um único texto de consulta poderá gerar várias entradas de consulta se elas forem executadas em configurações de contextos diferentes ou se forem executadas fora versus dentro de diferentes módulos do [!INCLUDE[tsql](../../includes/tsql-md.md)] (procedimentos armazenados, gatilhos etc.).|  
|**sys.query_store_plan**|Apresenta estimativa de plano para a consulta com as estatísticas de tempo de compilação. O plano armazenado é equivalente a um que você obteria usando o `SET SHOWPLAN_XML ON`.|  
|**sys.query_store_runtime_stats_interval**|O Repositório de Consultas divide o tempo em janelas de tempo geradas automaticamente (intervalos) e armazena estatísticas agregadas no intervalo para cada plano executado. O tamanho do intervalo é controlado pela opção de configuração Intervalo de Coleta de Estatísticas (em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) ou `INTERVAL_LENGTH_MINUTES` usando [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**sys.query_store_runtime_stats**|Estatísticas agregadas de tempo de execução para planos executados. Todas as métricas capturadas são expressas na forma de quatro funções estatísticas: Média, Mínimo, Máximo e Desvio Padrão.|  
  
 Para obter mais informações sobre modos de exibição do Repositório de Consultas, confira a seção **Exibições, funções e procedimentos relacionados** de [Monitorando o desempenho com o repositório de consultas](monitoring-performance-by-using-the-query-store.md).  
  
## <a name="query-processing"></a>Query Processing  
 O Repositório de Consultas interage com o pipeline de processamento de consulta nos pontos-chave a seguir:  
  
1.  Quando a consulta é compilada pela primeira vez, o texto de consulta e o plano inicial são enviados ao Repositório de Consultas  
  
2.  Quando a consulta é recompilada, isso significa que o plano está sendo atualizado no Repositório de Consultas. Se for criado um novo plano, o repositório de consultas adiciona a nova entrada de plano para a consulta, mantendo os anteriores juntos com suas estatísticas de execução.  
  
3.  Após a execução da consulta, as estatísticas de tempo de execução são enviadas para o Repositório de Consultas. O Repositório de Consultas mantém estatísticas agregadas precisas para cada plano que foi executado dentro do intervalo ativo no momento.  
  
4.  Durante a compilação e a verificação das fases de recompilação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determina se há um plano no Repositório de Consultas que deve ser aplicado para a consulta em execução no momento. Se houver um plano forçado e o plano no cache de procedimento for diferente dele, a consulta será recompilada, efetivamente da mesma forma como se PLAN HINT tiver sido aplicado à consulta. Esse processo acontece de forma transparente para o usuário.  
  
 O diagrama a seguir mostra os pontos de integração explicados acima:  
  
 ![query-store-process-2processor](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor")  
  
 Para minimizar a sobrecarga de E/S, novos dados são capturados na memória. As operações de gravação são enfileiradas e liberadas para o disco posteriormente. Consultas e informações do plano (Repositório de planos no diagrama abaixo) são liberados com latência mínima. As estatísticas de tempo de execução (Estatísticas de tempo de execução) são mantidas na memória por um período definido com a opção `DATA_FLUSH_INTERVAL_SECONDS` da instrução `SET QUERY_STORE` . A caixa de diálogo Repositório de Consultas do SSMS permite inserir um **Intervalo de liberação de dados (minutos)** , que é convertido para segundos.  
  
 ![query-store-process-3plan](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan")  
  
 Se o sistema falhar, o Repositório de Consultas poderá perder dados de tempo de execução até a quantidade definida com `DATA_FLUSH_INTERVAL_SECONDS`. O valor padrão de 900 segundos (15 minutos) é um bom equilíbrio entre desempenho de captura de consulta e a disponibilidade de dados.  
Se o sistema estiver enfrentando pressão de memória, as estatísticas de tempo de execução poderão ser liberadas para o disco antes do que foi definido com `DATA_FLUSH_INTERVAL_SECONDS`.  
Durante a leitura do Repositório de Consultas, os dados na memória e no disco são unificados de maneira transparente.
Se uma sessão for encerrada ou o aplicativo cliente for reiniciado ou falhar, as estatísticas de consulta não serão gravadas.  
  
 ![query-store-process-4planinfo](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
