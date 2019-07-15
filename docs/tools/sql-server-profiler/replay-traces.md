---
title: Repetir rastreamentos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, replaying traces
- Run to Cursor option
- Toggle Breakpoint option
- traces [SQL Server], replaying
- replaying traces
- playback engine [SQL Server Profiler]
- events [SQL Server], replaying traces
- Profiler [SQL Server Profiler], replaying traces
ms.assetid: da958d3c-7f3e-44c9-aecc-8a9493bea7c0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fe0132fa04e2201a66c64e672b074d380a831b94
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733379"
---
# <a name="replay-traces"></a>Repetir rastreamentos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Reprodução é a capacidade para reproduzir a atividade que foi capturada em um rastreamento. Ao criar ou editar um rastreamento, você pode salvá-lo em um arquivo para reproduzi-lo posteriormente. Você pode usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para reproduzir a atividade de rastreamento de um único computador. Para cargas de trabalho grandes, use o Distributed Replay Utility para reproduzir dados de rastreamento de vários computadores.  
  
 Esta seção descreve como usar os recursos de reprodução do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Para obter mais informações sobre o Distributed Replay Utility, consulte [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] apresenta um mecanismo de repetição multi-threaded que consegue simular as conexões de usuário e a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A repetição é útil para solucionar problemas de aplicativos ou processos. Tendo identificado o problema e implementado correções, execute o rastreamento que encontrou o problema potencial contra o aplicativo ou processo corrigido. Em seguida, repita o rastreamento original e compare os resultados.  
  
 A repetição de rastreamentos dá suporte à depuração por meio das opções **Alternar Ponto de Interrupção** e **Executar até o Cursor** do menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Replay** menu. Essas opções melhoram, em especial, a análise de scripts longos, pois elas podem dividir a repetição do rastreamento em segmentos curtos que podem ser analisados incrementalmente.  
  
 Para obter informações sobre as permissões necessárias para reproduzir rastreamentos, consulte [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Requisitos para repetição](../../tools/sql-server-profiler/replay-requirements.md)|Descreve os eventos que devem ser incluídos na definição de um rastreamento para que ele possa ser reproduzido com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Opções de repetição &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-options-sql-server-profiler.md)|Descreve as opções que podem ser definidas na caixa de diálogo **Configuração de Reprodução** do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Considerações para reproduzir rastreamentos &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)|Descreve os eventos de rastreamento que não podem ser reproduzidos com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e os efeitos da reprodução de rastreamentos no desempenho do servidor.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
