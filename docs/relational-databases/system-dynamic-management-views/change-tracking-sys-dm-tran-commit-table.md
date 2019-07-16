---
title: DM tran_commit_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4bd5b497f1d96f813570282f785fe0cbfe73265d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017932"
---
# <a name="change-tracking---sysdmtrancommittable"></a>Controle de alterações - DM tran_commit_table
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Exibe uma linha para cada transação confirmada para uma tabela controlada pelo controle de alterações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A exibição de gerenciamento de sys.dm_tran_commit_table, que é fornecida para fins de suporte e expõe as informações relacionadas a transações que o controle de alterações armazena na tabela do sistema sys.syscommittab. A tabela sys.syscommittab fornece um mapeamento persistente eficiente de uma ID de transação específica ao banco de dados para o LSN (número de sequência de log) de confirmação da transação e para o carimbo de data/hora da confirmação. Os dados armazenados na tabela sys.syscommittab e expostos nessa exibição de gerenciamento estão sujeitos à limpeza de acordo com o período de retenção especificado quando o controle de alterações foi configurado.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_tran_commit_table**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|commit_ts|**bigint**|Um número que aumenta de forma monotônica que serve como um carimbo de data/hora específico a um banco de dados para cada transação confirmada.|  
|xdes_id|**bigint**|Uma ID interna específica do banco de dados para a transação.|  
|commit_lbn|**bigint**|O número do bloco de logs que contém o registro de log de confirmação para a transação.|  
|commit_csn|**bigint**|O número de sequência de confirmação específico da instância para a transação.|  
|commit_time|**smalldatetime**|A hora em que a transação foi confirmada.|  
|pdw_node_id|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sobre o controle de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


