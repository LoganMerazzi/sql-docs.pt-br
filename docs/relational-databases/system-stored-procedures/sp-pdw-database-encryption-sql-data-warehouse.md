---
title: sp_pdw_database_encryption (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 47d7aca62ddbf2637b54d77171a08817b842555c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008916"
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>sp_pdw_database_encryption (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_database_encryption** para habilitar a transparent data encryption para uma [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] appliance. Quando **sp_pdw_database_encryption** definido como 1, use o **ALTER DATABASE** instrução para criptografar um banco de dados usando TDE.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>Parâmetros  
`[ @enabled = ] enabled` Determina se a criptografia transparente de dados está habilitada. *habilitada* está **int**, e pode ser um dos seguintes valores:  
  
-   0 = Desabilitado  
  
-   1 = Habilitado  
  
 Executando **sp_pdw_database_encryption** sem parâmetros reverte o estado atual da TDE no dispositivo como um conjunto de resultados escalares: 0 para desabilitado ou 1 para habilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando a TDE é habilitada por meio **sp_pdw_database_encryption**, banco de dados tempdb é descartado, recriado e criptografado. Por esse motivo, a TDE não pode ser habilitada em um dispositivo, embora haja outras sessões ativas usando o tempdb. Habilitando ou desabilitando a TDE em um dispositivo é uma ação que altera o estado do dispositivo, na maioria dos casos é esperada para ser executada uma vez no tempo de vida de dispositivo e deve ser executada quando não há nenhum tráfego no dispositivo.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **sysadmin** função de banco de dados fixa ou **CONTROL SERVER** permissão.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita a TDE no dispositivo.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
