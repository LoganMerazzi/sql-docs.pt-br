---
title: sys. resource_stats (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 06e3a3e632473c33a3f4652b2f4169ce3c7ca1e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097047"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna os dados de armazenamento e de utilização da CPU para um Banco de Dados SQL do Azure. Os dados são coletados e agregados em intervalos de cinco minutos. Para cada banco de dados do usuário, há uma linha para cada janela de relatório de cinco minutos em que há uma alteração no consumo de recursos. Os dados retornados incluem o uso da CPU, alteração do tamanho do armazenamento e banco de dados de alteração de SKU. Bancos de dados ociosos sem alterações não podem ter linhas para cada intervalo de cinco minutos. Os dados históricos são retidos por aproximadamente 14 dias.  
  
 O **sys. resource_stats** exibição tem definições diferentes dependendo da versão do servidor do banco de dados SQL Azure que o banco de dados está associado. Considere essas diferenças e quaisquer modificações que seu aplicativo exige ao fazer a atualização para uma nova versão do servidor.  
  
 A tabela a seguir descreve as colunas disponíveis em um servidor v12:  
  
|Colunas|Tipo de dados|Descrição|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora UTC que indica o início do intervalo de relatório de cinco minutos.|  
|end_time|**datetime**|Hora UTC que indica o final do intervalo de relatório de cinco minutos.|  
|database_name|**varchar**|Nome do banco de dados do usuário.|  
|sku|**varchar**|Camada de serviço do banco de dados. O valores possíveis são os seguintes:<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br />Uso Geral<br /><br />Comercialmente Crítica|  
|storage_in_megabytes|**float**|Tamanho máximo de armazenamento em megabytes para o período de tempo, incluindo o banco de dados, índices, procedimentos armazenados e metadados.|  
|avg_cpu_percent|**numeric**|Utilização média de computação, em porcentagem, do limite da camada de serviço.|  
|avg_data_io_percent|**numeric**|Utilização média de E/S em percentagem com base no limite da camada de serviço.|  
|avg_log_write_percent|**numeric**|Utilização média do recurso de gravação, em porcentagem, do limite da camada de serviço.|  
|max_worker_percent|**decimal(5,2)**|Máximo de trabalhos simultâneos (solicitações) em porcentagem do limite da camada de serviço do banco de dados.<br /><br /> Máximo está atualmente calculado para o intervalo de cinco minutos, com base nos exemplos de trabalho simultâneos contagens de 15 segundos.|  
|max_session_percent|**decimal(5,2)**|Máximo de sessões simultâneas em percentual, com base no limite da camada de serviço do banco de dados.<br /><br /> Máximo está atualmente calculado para o intervalo de cinco minutos, com base em amostras de 15 segundos de contagens de sessões simultâneas.|  
|dtu_limit|**int**|Banco de dados max DTU configuração atual para este banco de dados durante esse intervalo. |  
|allocated_storage_in_megabytes|**float**|A quantidade de formatado espaço de arquivo em MB disponibilizada para armazenar dados do banco de dados. Espaço de arquivo formatado também é chamado de espaço de dados alocado.  Para obter mais informações, consulte: [Gerenciamento de espaço de arquivo no banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  Para obter mais contexto sobre esses limites e as camadas de serviço, consulte os tópicos [camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/).  
    
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Os dados retornados pelo **sys. resource_stats** é expresso como uma porcentagem dos limites máximos permitidos para o nível de desempenho/camada de serviço que você está executando.  
  
 Quando um banco de dados é um membro de um pool Elástico, as estatísticas de recursos apresentadas como valores de porcentagem são expressas como a porcentagem do limite máximo para os bancos de dados, conforme definido na configuração do pool Elástico.  
  
 Para obter uma exibição mais granular desses dados, use **sys.DM db_resource_stats** exibição de gerenciamento dinâmico em um banco de dados do usuário. Essa visualização captura dados a cada 15 segundos e mantém dados históricos por 1 hora.  Para obter mais informações, consulte [sys.DM db_resource_stats &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os bancos de dados que estão com média de pelo menos 80% de utilização de computação durante a última semana.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>Consulte também  
 [Camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Limites e recursos de camada de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
