---
title: sys.dm_db_mirroring_auto_page_repair (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair
- dm_db_mirroring_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- automatic page repair
- database mirroring [SQL Server], automatic page repair
- sys.dm_db_mirroring_auto_page_repair dynamic management view
ms.assetid: 49f0fc2a-e25e-47e1-a135-563adb509af1
author: stevestein
ms.author: sstein
ms.openlocfilehash: e08aa031af0bd8c9d5c5ad012d11c534281f92f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017911"
---
# <a name="database-mirroring---sysdmdbmirroringautopagerepair"></a>-O espelhamento de banco de dados sys.dm_db_mirroring_auto_page_repair
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada tentativa de reparo automático de página em qualquer banco de dados espelho na instância de servidor. Essa exibição contém linhas para as últimas tentativas de conserto de página automático em um determinado banco de dados espelho, com um máximo de 100 linhas por banco de dados. Assim que o banco de dados atinge o máximo, a linha de sua próxima tentativa de conserto de página automático substitui uma das entradas existentes. A tabela a seguir define o significado das diversas colunas.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados ao qual corresponde a linha.|  
|**file_id**|**int**|ID do arquivo em que a página está localizada.|  
|**page_id**|**bigint**|ID da página no arquivo.|  
|**error_type**|**int**|O tipo de erro. Os valores podem ser:<br /><br /> **-** 1 = todos os erros de hardware 823<br /><br /> 1 = 824 erros que não seja uma soma de verificação inválida ou uma página interrompida (como uma ID de página inválida)<br /><br /> 2 = Soma de verificação inválida<br /><br /> 3 = Página interrompida|  
|**page_status**|**int**|O status da tentativa de conserto da página:<br /><br /> 2 = Enfileirada para solicitação do parceiro.<br /><br /> 3 = Solicitação enviada ao parceiro.<br /><br /> 4 = Enfileirada para conserto de página automático (resposta recebida do parceiro).<br /><br /> 5 = Conserto de página automático efetuado com êxito; a página deve estar utilizável.<br /><br /> 6 = Irreparável. Isso indica que ocorreu um erro durante a tentativa do conserto da página, por exemplo, porque a página também está corrompida no parceiro, o parceiro está desconectado ou houve um problema de rede. Esse estado não é terminal; se o dano for encontrado novamente na página, a página será novamente solicitada ao parceiro.|  
|**modification_time**|**datetime**|Hora da última alteração no estado da página.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Reparo automático de página &#40;Grupos de Disponibilidade: Espelhamento de banco de dados&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  


