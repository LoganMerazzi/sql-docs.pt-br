---
title: sys.column_master_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ae8a4077c0fe4e3f6b7754b4fc53a401d03e355
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140057"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada chave mestra de banco de dados adicionada usando o [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) instrução. Cada linha representa uma chave mestra de coluna única (CMK).  
    
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome da CMK.|  
|**column_master_key_id**|**int**|ID da chave mestra de coluna.|  
|**create_date**|**datetime**|Data em que a chave mestra de coluna foi criada.|  
|**modify_date**|**datetime**|Data em que a chave mestra de coluna foi modificado pela última vez.|  
|**key_store_provider_name**|**sysname**|Nome do provedor para o repositório de chave mestra de coluna que contém a CMK. Os valores permitidos são:<br /><br /> MSSQL_CERTIFICATE_STORE - se o repositório de chave mestra de coluna for um certificado de Store.<br /><br /> Um valor definido pelo usuário, se o repositório de chave mestra de coluna for de um tipo personalizado.|  
|**key_path**|**nvarchar(4000)**|Um caminho de store específicas de chave mestra de coluna da chave. O formato do caminho depende do tipo de repositório de chave mestra de coluna. Exemplo:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> Para um repositório de chaves mestras de coluna personalizada, o desenvolvedor é responsável por definir um caminho de chave que é para o repositório de chave mestra de coluna personalizado.|  
|**allow_enclave_computations**|**bit**|Indica se a chave mestra de coluna é enclave habilitado, (se chaves de criptografia de coluna, criptografadas com essa chave mestre, podem ser usadas para cálculos de enclaves seguras do lado do servidor). Para obter mais informações, consulte [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).|  
|**signature**|**varbinary(max)**|Uma assinatura digital da **key_path** e **allow_enclave_computations**, produzido usando-se a chave mestra de coluna, referenciado pelo **key_path**.|


  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW ANY COLUMN MASTER KEY** permissão.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
