---
title: Rastreando e reproduzindo eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f441cceed84b873b31c7d4691b08a541a0aee06f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030163"
---
# <a name="tracing-and-replaying-events"></a>Rastreando e reproduzindo eventos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  No SMO, o **rastreamento** e **Replay** objetos no <xref:Microsoft.SqlServer.Management.Trace> namespace fornecem acesso programático para o [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] funcionalidade, que é usada para monitorar uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ou [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Você pode capturar e salvar dados sobre cada evento em um arquivo ou tabela para análise posterior. Por exemplo, é possível monitorar um ambiente de produção para observar quais procedimentos estão impedindo o desempenho devido à lentidão na execução.  
  
 Os objetos **Trace** e **Replay** fornecem um conjunto de objetos que podem ser usados para criar rastreamentos em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses objetos podem ser usados de dentro dos seus aplicativos para criar rastreamentos manualmente para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Além disso, o os objetos **Trace** de SMO podem ser usados para ler arquivos e tabelas de Rastreamento do SQL que foram criadas monitorando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], o or DTS logging.  
  
 Os objetos **Trace** de SMO permitem que você execute estas funções:  
  
-   Criar um rastreamento.  
  
-   Definir os filtros no rastreamento.  
  
-   Definir os eventos que estão sendo localizados.  
  
-   Interromper ou iniciar um rastreamento.  
  
-   Ler arquivos e tabelas de rastreamento.  
  
-   Obter informações sobre eventos em um rastreamento.  
  
-   Obter informações sobre filtros em um rastreamento.  
  
-   Manipular dados de rastreamento programaticamente.  
  
-   Escrever tabelas e arquivos de rastreamento.  
  
-   Reproduzir arquivos ou tabelas de rastreamento.  
  
 Os dados de rastreamento dos objetos **Trace** e **Replay** podem ser usados pelo aplicativo de SMO ou podem ser examinados manualmente usando [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). Os dados de rastreamento também são compatíveis com os procedimentos armazenados [SQL Trace](../../../relational-databases/sql-trace/sql-trace.md) que também fornecem capacidades de rastreamento.  
  
 Os objetos de rastreamento SMO residem no namespace <xref:Microsoft.SqlServer.Management.Trace>, que requer uma referência ao arquivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
 O **rastreamento** e **Replay** objetos requerem uma [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> objeto para estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto reside na [Microsoft.SqlServer.Management.Common](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common) namespace, que requer uma referência para o arquivo de ConnectionInfo.  
  
> [!NOTE]  
>  Os objetos **Trace** e **Replay** não têm suporte em uma plataforma de 64 bits.  
  
  
