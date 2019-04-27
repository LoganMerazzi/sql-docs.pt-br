---
title: sys.dm_os_virtual_address_dump (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_virtual_address_dump
- sys.dm_os_virtual_address_dump_TSQL
- sys.dm_os_virtual_address_dump
- dm_os_virtual_address_dump_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_virtual_address_dump dynamic management view
ms.assetid: 7b24ea55-3873-42fd-a86c-441c92eb6175
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b12c9e533d404b01f896dd66ee046c9a9cd110d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628220"
---
# <a name="sysdmosvirtualaddressdump-transact-sql"></a>sys.dm_os_virtual_address_dump (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna informações sobre um intervalo de páginas no espaço de endereçamento virtual do processo de chamada.  
  
> [!NOTE]  
>  Essas informações também são retornadas pela **VirtualQuery** API do Windows.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_virtual_address_dump**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**region_base_address**|**varbinary(8)**|Ponteiro para o endereço base da região de páginas. Não permite valor nulo.|  
|**region_allocation_base_address**|**varbinary(8)**|Ponteiro para o endereço base de um intervalo de páginas alocado pela função VirtualAlloc da API do Windows. A página apontada pelo membro BaseAddress está contida nesse intervalo de alocação. Não permite valor nulo.|  
|**region_allocation_protection**|**varbinary(8)**|Atributos de proteção quando a região foi inicialmente alocada. O valor é um dos seguintes:<br /><br /> -   PAGE_READONLY<br />-   PAGE_READWRITE<br />-   PAGE_NOACCESS<br />-   PAGE_WRITECOPY<br />-   PAGE_EXECUTE<br />-   PAGE_EXECUTE_READ<br />-   PAGE_EXECUTE_READWRITE<br />-   PAGE_EXECUTE_WRITECOPY<br />-   PAGE_GUARD<br />-   PAGE_NOCACHE<br /><br /> Não permite valor nulo.|  
|**region_size_in_bytes**|**bigint**|Tamanho da região, em bytes, iniciando no endereço base no qual todas as páginas têm os mesmos atributos. Não permite valor nulo.|  
|**region_state**|**varbinary(8)**|O estado atual da região. Ele é um dos seguintes:<br /><br /> -   MEM_COMMIT<br />-   MEM_RESERVE<br />-   MEM_FREE<br /><br /> Não permite valor nulo.|  
|**region_current_protection**|**varbinary(8)**|Atributos de proteção. O valor é um dos seguintes:<br /><br /> -   PAGE_READONLY<br />-   PAGE_READWRITE<br />-   PAGE_NOACCESS<br />-   PAGE_WRITECOPY<br />-   PAGE_EXECUTE<br />-   PAGE_EXECUTE_READ<br />-   PAGE_EXECUTE_READWRITE<br />-   PAGE_EXECUTE_WRITECOPY<br />-   PAGE_GUARD<br />-   PAGE_NOCACHE<br /><br /> Não permite valor nulo.|  
|**region_type**|**varbinary(8)**|Identifica os tipos de páginas na região. O valor pode ser um dos seguintes:<br /><br /> -   MEM_PRIVATE<br />-   MEM_MAPPED<br />-   MEM_IMAGE<br /><br /> Não permite valor nulo.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


