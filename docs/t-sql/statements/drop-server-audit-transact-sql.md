---
title: DROP SERVER AUDIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SERVER AUDIT
- DROP_SERVER_AUDIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SERVER AUDIT statement
ms.assetid: faace8a3-daa9-4208-a2cd-4249eb32175c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f0bb90a3dd13ffd245c1cac5a9ee1610055aae55
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929280"
---
# <a name="drop-server-audit--transact-sql"></a>DROP SERVER AUDIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta um objeto de auditoria de servidor usando o recurso SQL Server Audit. Para obter mais informações sobre o SQL Server Audit, consulte [SQL Server Audit &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP SERVER AUDIT audit_name  
    [ ; ]  
```  
  
## <a name="remarks"></a>Remarks  
 Você deve definir o estado de uma auditoria para a opção OFF para efetuar alterações em uma auditoria. Se DROP AUDIT for executada quando uma auditoria estiver habilitada com qualquer opção diferente de STATE=OFF, você receberá uma mensagem de erro MSG_NEED_AUDIT_DISABLED.  
  
 Uma DROP SERVER AUDIT remove os metadados da auditoria, mas não os dados de auditoria que foram coletados antes da emissão do comando.  
  
 DROP SERVER AUDIT não descarta especificações de auditoria de banco de dados ou de servidor associado. Essas especificações devem ser descartadas manualmente ou deixadas órfãs e depois mapeadas para uma nova auditoria de servidor.  
  
## <a name="permissions"></a>Permissões  
 Para criar, alterar ou descartar uma Auditoria de Servidor, as entidades devem ter a permissão ALTER ANY SERVER AUDIT ou CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta uma auditoria denominada `HIPAA_Audit`.  
  
```  
ALTER SERVER AUDIT HIPAA_Audit  
STATE = OFF;  
GO  
DROP SERVER AUDIT HIPAA_Audit;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
