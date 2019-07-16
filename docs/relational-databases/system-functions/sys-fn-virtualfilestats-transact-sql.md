---
title: sys. fn_virtualfilestats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_virtualfilestats_TSQL
- fn_virtualfilestats
dev_langs:
- TSQL
helpviewer_keywords:
- I/O [SQL Server], statistics
- fn_virtualfilestats function
- sys.fn_virtualfilestats function
- statistical information [SQL Server], I/O
ms.assetid: 96b28abb-b059-48db-be2b-d60fe127f6aa
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aade9e02515e0d18e4edae188d72e5edafebbd3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059206"
---
# <a name="sysfnvirtualfilestats-transact-sql"></a>sys.fn_virtualfilestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna estatísticas de E/S para arquivos de banco de dados, incluindo arquivos de log. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essas informações também estão disponíveis a partir de [DM io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) exibição de gerenciamento dinâmico.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_virtualfilestats ( { database_id | NULL } , { file_id | NULL } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_id* | NULL  
 É a ID do banco de dados. *database_id* é **int**, sem padrão. Especifique NULL para retornar informações de todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *file_id* | NULL  
 É a ID do arquivo. *file_id* está **int**, sem padrão. Especifique NULL para retornar informações de todos os arquivos do banco de dados.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**DbId**|**smallint**|ID do banco de dados.|  
|**FileId**|**smallint**|ID do arquivo.|  
|**TimeStamp**|**bigint**|Carimbo de data/hora do banco de dados do qual os dados foram obtidos. **int** nas versões anteriores [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]. |  
|**NumberReads**|**bigint**|Número de leituras emitidas no arquivo.|  
|**BytesRead**|**bigint**|Número de bytes lidos emitidos no arquivo.|  
|**IoStallReadMS**|**bigint**|Período de tempo total, em milissegundos, que os usuários esperaram pela conclusão das E/Ss de leitura no arquivo.|  
|**NumberWrites**|**bigint**|Número de gravações feitas no arquivo.|  
|**BytesWritten**|**bigint**|Número de bytes gravados no arquivo.|  
|**IoStallWriteMS**|**bigint**|Período de tempo total, em milissegundos, que os usuários esperaram pela conclusão das E/Ss de gravação no arquivo.|  
|**IoStallMS**|**bigint**|Soma de **IoStallReadMS** e **IoStallWriteMS**.|  
|**FileHandle**|**bigint**|Valor do identificador de arquivo.|  
|**BytesOnDisk**|**bigint**|Tamanho do arquivo físico (contagem de bytes) em disco.<br /><br /> Para arquivos de banco de dados, isso é o mesmo valor que **tamanho** na **sys. database_files**, mas é expresso em bytes em vez de páginas.<br /><br /> Para arquivos esparsos de instantâneo do banco de dados, este é o espaço que o sistema operacional está usando para o arquivo.|  
  
## <a name="remarks"></a>Comentários  
 **fn_virtualfilestats** é um sistema de função com valor de tabela que fornece informações de estatísticas, como o número total de e/SS realizada em um arquivo. Você pode usar essa função para ajudar a manter o controle do período de tempo que os usuários esperaram para ler ou gravar em um arquivo. A função também ajuda a identificar os arquivos que encontram grande quantidade de atividade de E/S.  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-statistical-information-for-a-database"></a>A. Exibindo informações estatísticas para um banco de dados  
 O exemplo a seguir exibe informações estatísticas para o ID de arquivo 1 no banco de dados com um ID `1`.  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(1, 1);  
GO  
```  
  
### <a name="b-displaying-statistical-information-for-a-named-database-and-file"></a>B. Exibindo informações estatísticas para um banco de dados e arquivo nomeados  
 O exemplo a seguir exibe informações estatísticas para o arquivo de log no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A função de sistema `DB_ID` é usado para especificar o *database_id* parâmetro.  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="c-displaying-statistical-information-for-all-databases-and-files"></a>C. Exibindo informações estatísticas para todos os bancos de dados e arquivos  
 O exemplo a seguir exibe informações estatísticas para todos os arquivos em todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(NULL,NULL);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)   
 [FILE_IDEX &#40;Transact-SQL&#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
