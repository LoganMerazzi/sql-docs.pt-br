---
title: sys. assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assemblies
- assemblies_TSQL
- sys.assemblies_TSQL
- assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assemblies catalog view
ms.assetid: e321753f-293f-42ab-b225-d118713df40b
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 19577afb746e3b005dffd803d86351d8a4b0eca4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001210"
---
# <a name="sysassemblies-transact-sql"></a>sys.assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna uma linha para cada assembly.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do assembly. É exclusiva no banco de dados.|  
|**principal_id**|**int**|ID da entidade que é proprietária desse assembly.|  
|**assembly_id**|**int**|Número de identificação de assembly. É exclusivo em um banco de dados.|  
|**clr_name**|**nvarchar(4000)**|Cadeia de caracteres canônica que codifica o nome simples, o número de versão, a cultura, a chave pública e a arquitetura do assembly. Esse valor identifica exclusivamente o assembly no lado CLR (Common Language Runtime).|  
|**permission_set**|**tinyint**|Conjunto de permissões/nível de segurança do assembly.<br /><br /> 1 = Acesso seguro<br /><br /> 2 = Acesso externo<br /><br /> 3 = Acesso não seguro|  
|**permission_set_desc**|**nvarchar(60)**|Descrição do conjunto de permissões/nível de segurança do assembly.<br /><br /> SAFE_ACCESS<br /><br /> EXTERNAL_ACCESS<br /><br /> UNSAFE_ACCESS|  
|**is_visible**|**bit**|1 = Assembly é visível para registrar pontos de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)].<br /><br /> 0 = Assembly só é planejado para chamadores gerenciados. Ou seja, o assembly fornece implementação interna para outros assemblies do banco de dados.|  
|**create_date**|**datetime**|Data em que o assembly foi criado ou registrado.|  
|**modify_date**|**datetime**|Data em que o assembly foi modificado.|  
|**is_user_defined**|**bit**|Indica a origem do assembly.<br /><br /> 0 = assemblies definidos pelo sistema (como Types para o **hierarchyid** tipo de dados)<br /><br /> 1 = Assemblies definidos pelo usuário|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do catálogo Assembly CLR &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
