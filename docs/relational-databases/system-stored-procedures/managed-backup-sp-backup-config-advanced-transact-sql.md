---
title: managed_backup.sp_backup_config_advanced (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_optional
- sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional
dev_langs:
- TSQL
helpviewer_keywords:
- sp_backup_config_optional
- managed_backup.sp_backup_config_optional
ms.assetid: 4fae8193-1f88-48fd-a94a-4786efe8d6af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cbbbfbf442d36a5f78771e4d097888a86b441065
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942143"
---
# <a name="managedbackupspbackupconfigadvanced-transact-sql"></a>managed_backup.sp_backup_config_advanced (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Define as configurações avançadas para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @database_name  
 O nome do banco de dados para habilitar o backup gerenciado em um banco de dados específico. Se for NULL ou *, em seguida, esse backup gerenciado se aplica a todos os bancos de dados no servidor.  
  
 @encryption_algorithm  
 O nome do algoritmo de criptografia usado durante o backup para criptografar o arquivo de backup. O @encryption_algorithm está **SYSNAME**. É um parâmetro obrigatório ao configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pela primeira vez para o banco de dados. Especificar **NO_ENCRYPTION** se você não quiser criptografar o arquivo de backup. Ao alterar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] definições de configuração, este parâmetro é opcional – se o parâmetro não for especificado, os valores de configuração existentes serão retidos. Os valores permitidos para este parâmetro são:  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 Para obter mais informações sobre algoritmos de criptografia, consulte [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md).  
  
 @encryptor_type  
 O tipo de Criptografador, que pode ser 'Certificado' ou ' ASYMMETRIC_KEY ". O @encryptor_type está **nvarchar(32)** . Esse parâmetro é opcional se você especificar NO_ENCRYPTION para o @encryption_algorithm parâmetro.  
  
 @encryptor_name  
 O nome de um certificado existente ou chave assimétrica a ser usado para criptografar o backup. O @encryptor_name está **SYSNAME**. Se estiver usando uma chave assimétrica, ela deverá ser configurada com EKM (gerenciamento de chave extensível). Esse parâmetro é opcional se você especificar NO_ENCRYPTION para o @encryption_algorithm parâmetro.  
  
 Para obter mais informações, veja [EKM &#40;Gerenciamento de Chave Extensível&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 @local_cache_path  
 Ainda não há suporte para esse parâmetro.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer associação na **db_backupoperator** função de banco de dados com **ALTER ANY CREDENTIAL** permissões, e **EXECUTE** permissões em **sp_delete backuphistory** procedimento armazenado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define as opções de configuração avançada para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a instância do SQL Server.  
  
```  
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
