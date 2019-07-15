---
title: Modificar um filtro (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2ed60fcbc794b9d1a0ef37ce6f5c76aa666e5059
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733089"
---
# <a name="modify-a-filter-sql-server-profiler"></a>Modificar um filtro (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os filtros são adicionados aos modelos de rastreamento, que contêm as definições de rastreamento, para limitar o número de eventos coletados por um rastreamento. Limitar o número de eventos coletados pode reduzir os efeitos do desempenho do rastreamento. Se definir filtros para um modelo de rastreamento e achar que o rastreamento não está coletando o tipo de informações de que necessita, você poderá editar o filtro.  
  
### <a name="to-modify-a-filter"></a>Para modificar um filtro  
  
1.  No [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], abra o modelo referente ao filtro de rastreamento que você deseja modificar. No menu **Arquivo** , clique em **Modelos**e escolha **Editar Modelo**.  
  
2.  Na guia **Geral** da caixa de diálogo **Propriedades do Modelo de Rastreamento** , selecione um modelo na lista **Selecionar nome do modelo** .  
  
3.  Clique na guia **Seleção de Eventos** .  
  
     A guia **Seleção de Eventos** contém um controle de grade. O controle de grade é uma tabela que contém cada uma das classes de evento rastreáveis. A tabela contém uma linha para cada classe de evento. As classes de evento podem diferir ligeiramente, dependendo do tipo e versão de servidor com o qual você está conectado. As classes de evento são identificadas na coluna **Events**da grade e são agrupadas por categoria de evento. As colunas restantes listam as colunas de dados que podem ser retornadas para cada classe de evento.  
  
4.  Clique em **Filtros de Coluna**.  
  
5.  Na caixa de diálogo **Editar Filtro** , clique no valor próximo ao operador de comparação que você deseja editar e exclua-o ou digite o novo valor. Você também pode adicionar outros filtros.  
  
6.  Clique em **OK** e salve o modelo.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
