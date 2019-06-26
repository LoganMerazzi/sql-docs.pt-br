---
title: sys.internal_partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5795ec9feaef483dd3ee9b5f3e31dbb619a89331
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388336"
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada conjunto de linhas que rastreia dados internos para índices columnstore em tabelas baseadas em disco. Esses conjuntos de linhas são internos para índices columnstore e delta, mapeamentos de grupo de linhas e linhas de faixa excluída armazenam rowgroups. Controle os dados para cada um para cada partição de tabela; cada tabela tem pelo menos uma partição. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recria os conjuntos de linhas de cada vez que ela recria o índice columnstore.   
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|ID de partição para essa partição. É exclusiva em um banco de dados.|  
|object_id|**int**|ID de objeto para a tabela que contém a partição.|  
|index_id|**int**|ID de índice para o índice columnstore definido na tabela.<br /><br /> 1 = índice columnstore clusterizado<br /><br /> 2 = índice columnstore não clusterizado|  
|partition_number|**int**|O número da partição.<br /><br /> 1 = a primeira partição de uma tabela particionada, ou a única partição de uma tabela não particionada.<br /><br /> 2 = segunda partição e assim por diante.|  
|internal_object_type|**tinyint**|Objetos de conjunto de linhas que acompanham os dados internos para o índice columnstore.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP - este índice de bitmap controla linhas que são marcadas como excluídas do columnstore. O bitmap é para cada grupo de linhas, pois as partições podem ter linhas em múltiplos rowgroups. As linhas são que ainda estão fisicamente presentes e ocupando espaço no columnstore.<br /><br /> COLUMN_STORE_DELTA_STORE - grupos de armazenamentos de linhas, chamados de rowgroups, que não foi compactado para o armazenamento Colunar. Cada partição de tabela pode ter zero ou mais rowgroups do deltastore.<br /><br /> COLUMN_STORE_DELETE_BUFFER - para manter as exclusões para os índices columnstore não clusterizados atualizáveis. Quando uma consulta exclui uma linha da tabela rowstore base, o buffer de exclusão rastreia a exclusão do columnstore. Quando o número de linhas excluídas exceder 1048576, eles são mesclados novamente no bitmap delete por Tuple Mover thread em segundo plano ou por um comando Reorganize explícito.  Em qualquer ponto no tempo, a união entre o bitmap de exclusão e o buffer de exclusão representa linhas excluídas tudo.<br /><br /> COLUMN_STORE_MAPPING_INDEX - usado somente quando o índice columnstore clusterizado tem um índice não clusterizado secundário. Isso mapeia chaves de índice não clusterizado para o rowgroup correto e a ID de linha no columnstore. Ele apenas armazena as chaves de linhas que se movem para um grupo de linhas diferente; Isso ocorre quando um rowgroup delta é compactado no columnstore, e quando uma operação de mesclagem mescla linhas de dois rowgroups diferentes.|  
|Row_group_id|**int**|ID do rowgroup deltastore. Cada partição de tabela pode ter zero ou mais rowgroups do deltastore.|  
|hobt_id|**bigint**|ID do objeto interno do conjunto de linhas. Isso é uma boa chave para unir com outros DMVs para obter mais informações sobre as características físicas do conjunto de linhas interno.|  
|rows|**bigint**|Número aproximado de linhas nesta partição.|  
|data_compression|**tinyint**|O estado de compactação para o conjunto de linhas:<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|O estado de compactação para cada partição. Os valores possível para as tabelas rowstore são NONE, ROW e PAGE. Os valores possível para as tabelas columnstor são COLUMNSTORE e COLUMNSTORE_ARCHIVE.|  
|optimize_for_sequential_key|**bit**|1 = partição tiver a otimização de inserção de última página habilitada.<br><br>0 = valor padrão. Partição tiver a otimização da última página insert desabilitada.|
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="general-remarks"></a>Comentários gerais  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria novos índices de columnstore interno novamente cada vez que ele cria ou recria um índice columnstore.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. Exibir todos os conjuntos de linhas internos para uma tabela  
 Este exemplo retorna todos os conjuntos de linhas columnstore interno para uma tabela. Você também pode usar o hobt_id para obter mais informações sobre o conjunto de linhas específica.  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
