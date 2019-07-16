---
title: sp_helpstats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpstats
- sp_helpstats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpstats
ms.assetid: 00ab3cfd-2736-4fc0-b1b2-16dd49fb2fe5
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fba09255204b796a5134e8b8098e650430b7de63
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048399"
---
# <a name="sphelpstats-transact-sql"></a>sp_helpstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações de estatísticas sobre colunas e índices na tabela especificada.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] Para obter informações sobre estatísticas, consulte o [sys. Stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) e [sys. stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) exibições do catálogo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpstats[ @objname = ] 'object_name'   
     [ , [ @results = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'object_name'` Especifica a tabela na qual fornecer informações de estatísticas. *object_name* está **nvarchar(520)** e não pode ser nulo. Um nome de uma ou duas partes pode ser especificado.  
  
`[ @results = ] 'value'` Especifica a extensão de informações para fornecer. As entradas válidas são **todos os** e **estatísticas**. **Todos os** lista estatísticas para todos os índices e também as colunas que têm as estatísticas criadas; **STATS** lista apenas estatísticas não associadas a um índice. *valor* está **nvarchar (5)** com um padrão de STATS.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A tabela a seguir descreve as colunas do conjunto de resultados.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**statistics_name**|O nome das estatísticas. Retorna **sysname** e não pode ser nulo.|  
|**statistics_keys**|As chaves nas quais estatísticas são baseadas. Retorna **nvarchar(2078)** e não pode ser nulo.|  
  
## <a name="remarks"></a>Comentários  
 Use DBCC SHOW_STATISTICS para exibir informações de estatísticas detalhadas sobre quaisquer índice particular ou estatísticas. Para obter mais informações, consulte [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41; ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) e [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte cria estatísticas de uma única coluna para todas as colunas elegíveis de todas as tabelas de usuário no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], executando `sp_createstats`. Então, `sp_helpstats` é executado para encontrar as estatísticas resultantes criadas na tabela `Customer`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_createstats;  
GO  
EXEC sp_helpstats   
@objname = 'Sales.Customer',  
@results = 'ALL';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `statistics_name               statistics_keys`  
  
 `----------------------------  ----------------`  
  
 `_WA_Sys_00000003_22AA2996     AccountNumber`  
  
 `AK_Customer_AccountNumber     AccountNumber`  
  
 `AK_Customer_rowguid           rowguid`  
  
 `CustomerType                  CustomerType`  
  
 `IX_Customer_TerritoryID       TerritoryID`  
  
 `ModifiedDate                  ModifiedDate`  
  
 `PK_Customer_CustomerID        CustomerID`  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
