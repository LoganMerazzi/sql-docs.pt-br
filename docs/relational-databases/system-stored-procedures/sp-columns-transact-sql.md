---
title: sp_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_TSQL
- sp_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns
ms.assetid: 2dec79cf-2baf-4c0f-8cbb-afb1a8654e1e
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8eb18a81ff7910418e5b3c8a3b36a0e4cd94cc36
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070351"
---
# <a name="spcolumns-transact-sql"></a>sp_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna as informações de colunas dos objetos especificados que podem ser consultados no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_columns [ @table_name = ] object  
     [ , [ @table_owner = ] owner ]   
     [ , [ @table_qualifier = ] qualifier ]   
     [ , [ @column_name = ] column ]   
     [ , [ @ODBCVer = ] ODBCVer ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ \@table_name = ] object` É o nome do objeto que é usado para retornar informações de catálogo. *objeto* pode ser uma tabela, exibição ou outro objeto que tem colunas como funções com valor de tabela. *objeto* está **nvarchar(384)** , sem padrão. Há suporte para a correspondência do padrão curinga.  
  
`[ \@table_owner = ] owner` É o proprietário do objeto do objeto que é usado para retornar informações de catálogo. *proprietário* está **nvarchar(384)** , com um padrão NULL. Há suporte para a correspondência do padrão curinga. Se *proprietário* não é especificado, serão aplicadas as regras de visibilidade do objeto padrão do DBMS subjacente.  
  
 Se o usuário atual possuir um objeto com o nome especificado, as colunas desse objeto serão retornadas. Se *proprietário* não for especificado e o usuário atual não possuir um objeto com especificado *objeto*, **sp_columns** procurará um objeto com especificado  *objeto* pertencente ao proprietário do banco de dados. Se existir, as colunas desse objeto serão retornadas.  
  
`[ \@table_qualifier = ] qualifier` É o nome do qualificador do objeto. *qualificador* está **sysname**, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para objetos (_qualificador_ **.** _proprietário_ **.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ela representa o nome do servidor do ambiente de banco de dados do objeto.  
  
`[ \@column_name = ] column` É uma única coluna e é usada quando somente uma coluna de informações de catálogo é desejada. *coluna* está **nvarchar(384)** , com um padrão NULL. Se *coluna* não é especificado, todas as colunas são retornadas. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *coluna* representa o nome da coluna conforme listado na **syscolumns** tabela. Há suporte para a correspondência do padrão curinga. Para interoperabilidade máxima, o cliente de gateway deve pressupor correspondência apenas do padrão SQL-92 (os caracteres curinga % e _).  
  
`[ \@ODBCVer = ] ODBCVer` É a versão do ODBC que está sendo usado. *ODBCVer* está **int**, com um padrão de 2. Isto indica ODBC versão 2. Os valores válidos são 2 ou 3. Para as diferenças de comportamento entre as versões 2 e 3, consulte o ODBC **SQLColumns** especificação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O **sp_columns** procedimento armazenado de catálogo é equivalente a **SQLColumns** no ODBC. Os resultados retornados são ordenados por **TABLE_QUALIFIER**, **TABLE_OWNER**, e **TABLE_NAME**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nome do qualificador do objeto. Esse campo pode ser NULL.|  
|**TABLE_OWNER**|**sysname**|Nome do proprietário do objeto. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome do objeto. Esse campo sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna para cada coluna do **TABLE_NAME** retornado. Esse campo sempre retorna um valor.|  
|**DATA_TYPE**|**smallint**|Código inteiro para o tipo de dados do ODBC. Se este for um tipo de dados que não pode ser mapeado para um tipo do ODBC, ele será NULL. O nome do tipo de dados nativo é retornado na **TYPE_NAME** coluna.|  
|**TYPE_NAME**|**sysname**|Cadeia de caracteres que representa um tipo de dados. O DBMS subjacente apresenta este nome de tipo de dados.|  
|**PRECISION**|**int**|Número de dígitos significativos. O valor retornado para o **precisão** coluna está na base 10.|  
|**LENGTH**|**int**|Tamanho da transferência dos dados. <sup>1</sup>|  
|**ESCALA**|**smallint**|Número de dígitos à direita da vírgula decimal.|  
|**RADIX**|**smallint**|Base para tipos de dados numéricos.|  
|**PERMITE VALOR NULO**|**smallint**|Especifica possibilidade de nulidade:<br /><br /> 1 = NULL é possível.<br /><br /> 0 = NOT NULL.|  
|**COMENTÁRIOS**|**varchar(254)**|Esse campo sempre retorna NULL.|  
|**COLUMN_DEF**|**nvarchar(4000)**|Valor padrão da coluna.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados SQL conforme exibido no campo TYPE do descritor. Esta coluna é igual a **DATA_TYPE** coluna, exceto para o **datetime** e SQL-92 **intervalo** tipos de dados. Esta coluna sempre retorna um valor.|  
|**SQL_DATETIME_SUB**|**smallint**|Código de subtipo para **datetime** e o SQL-92 **intervalo** tipos de dados. Para outros tipos de dados, esta coluna retorna NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Comprimento máximo em bytes de uma coluna do tipo de dados caractere ou inteiro. Para todos os outros tipos de dados, esta coluna retorna NULL.|  
|**ORDINAL_POSITION**|**int**|Posição ordinal da coluna no objeto. A primeira coluna no objeto é 1. Esta coluna sempre retorna um valor.|  
|**IS_NULLABLE**|**varchar(254)**|A nulidade da coluna no objeto. As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> YES = A coluna pode incluir NULLS.<br /><br /> NO = A coluna não pode incluir NULLS.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> O valor retornado para essa coluna é diferente do valor retornado para o **NULLABLE** coluna.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados por procedimentos armazenados estendidos. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
 <sup>1</sup> para obter mais informações, consulte a documentação do Microsoft ODBC.  
  
## <a name="permissions"></a>Permissões  
 Requer permissões SELECT e VIEW DEFINITION no esquema.  
  
## <a name="remarks"></a>Comentários  
 **sp_columns** segue os requisitos para identificadores delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações de coluna para uma tabela especificada.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna informações de coluna para uma tabela especificada.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [Procedimentos armazenados do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


