---
title: sp_pkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ed0e041a6aa36027613059f16f3902bdb664aeb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056417"
---
# <a name="sppkeys-transact-sql"></a>sp_pkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de chave primária para uma única tabela no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_name= ] '*name*'  
 É a tabela para o qual retornar informações. *nome da* está **sysname**, sem padrão. Não há suporte para a correspondência de padrão curinga.  
  
 [ @table_owner=] '*proprietário*'  
 Especifica o proprietário da tabela especificada. *proprietário* está **sysname**, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Se *proprietário* não for especificado, serão aplicadas as regras de visibilidade de tabela padrão do DBMS subjacente.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se o *proprietário* não for especificado e o usuário atual não possuir uma tabela com especificado *nome*, esse procedimento procurará uma tabela com especificado *nome* pertencentes a proprietário do banco de dados. Caso exista, as colunas dessa tabela serão retornadas.  
  
 [ @table_qualifier=] '*qualificador*'  
 É o qualificador da tabela. *qualificador* está **sysname**, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (_qualificador_ **.** _proprietário_ **.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nome do qualificador da tabela. Esse campo pode ser NULL.|  
|TABLE_OWNER|**sysname**|Nome do proprietário da tabela. Esse campo sempre retorna um valor.|  
|TABLE_NAME|**sysname**|Nome da tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome da tabela, conforme listado na tabela sysobjects. Esse campo sempre retorna um valor.|  
|COLUMN_NAME|**sysname**|Nome da coluna, para cada coluna do TABLE_NAME retornado. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome da coluna conforme listado na tabela sys. Columns. Esse campo sempre retorna um valor.|  
|KEY_SEQ|**smallint**|Número de sequência da coluna em uma chave primária de várias colunas.|  
|PK_NAME|**sysname**|Identificador da chave primária. Retorna NULL se não for aplicável à fonte de dados.|  
  
## <a name="remarks"></a>Comentários  
 sp_pkeys retorna informações sobre colunas explicitamente definidas com uma restrição PRIMARY KEY. Como nem todos os sistemas oferecem suporte a chaves primárias explicitamente nomeadas, o implementador de gateway determina o que constitui uma chave primária. Observe que o termo chave primária refere-se a uma chave primária lógica para uma tabela. Espera-se que cada chave listada como chave primária lógica tenha um índice exclusivo definido. Esse índice exclusivo também é retornado no sp_statistics.  
  
 O procedimento armazenado de sp_pkeys é equivalente a SQLPrimaryKeys no ODBC. Os resultados retornados são ordenados por TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME e KEY_SEQ.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera a chaves primária para a tabela `HumanResources.Department` no banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir recupera a chaves primária para a tabela `DimAccount` no banco de dados `AdventureWorksPDW2012`. Ele retorna zero linhas indicando que a tabela não tem uma chave primária.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

