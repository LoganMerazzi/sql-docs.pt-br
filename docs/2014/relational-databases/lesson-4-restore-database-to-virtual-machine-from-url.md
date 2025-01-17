---
title: Lição 5. (Opcional) Criptografar o banco de dados usando TDE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7e78a787a67c430ec82bea4788fd1c92c4c72c4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090673"
---
# <a name="lesson-5-optional-encrypt-your-database-using-tde"></a>Lição 5. (Opcional) Criptografar o banco de dados usando TDE
  Como etapa opcional, você pode criptografar o banco de dados recém-criado. A criptografia transparente de dados (TDE) executa criptografia de E/S em tempo real e a descriptografia de dados e arquivos de log. Esse tipo de criptografia usa uma DEK (chave de criptografia do banco de dados), que é armazenada no registro de inicialização do banco de dados para disponibilidade durante a recuperação. Para obter mais informações, consulte [Transparent Data Encryption &#40;TDE&#41; ](security/encryption/transparent-data-encryption.md) e [mover um banco de dados protegido por TDE para outro SQL Server](security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
 Esta lição supõe que você já concluiu as seguintes etapas:  
  
-   Você tem uma conta de Armazenamento do Windows Azure.  
  
-   Você criou um contêiner na sua conta de Armazenamento do Windows Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial do SQL Server no computador de origem.  
  
-   Você criou um banco de dados seguindo as etapas descritas na lição 4.  
  
 Se você quiser criptografar um banco de dados, siga estas etapas:  
  
1.  Na máquina de origem, modifique e execute as seguintes instruções em uma janela de consulta:  
  
    ```  
  
    -- Create a master key and a server certificate   
    USE master   
    GO   
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01';   
    GO   
    CREATE CERTIFICATE MySQLCert WITH SUBJECT = 'SQL - Azure Storage Certification'   
    GO   
    -- Create a backup of the server certificate in the master database.   
    -- Store TDS certificates in the source machine locally.   
    BACKUP CERTIFICATE MySQLCert   
    TO FILE = 'C:\certs\MySQLCert.CER'   
    WITH PRIVATE KEY   
    (   
    FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
    ENCRYPTION BY PASSWORD = 'MySQLKey01'   
    );  
  
    ```  
  
2.  Em seguida, criptografe o novo banco de dados no computador de origem seguindo estas etapas:  
  
    ```  
  
    -- Switch to the new database.   
    -- Create a database encryption key, that is protected by the server certificate in the master database.    
    -- Alter the new database to encrypt the database using TDE.   
    USE TestDB1;   
    GO   
    -- Encrypt your database   
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE MySQLCert   
    GO   
  
    ALTER DATABASE TestDB1   
    SET ENCRYPTION ON   
    GO  
  
    ```  
  
 Se você quiser saber o estado de criptografia de um banco de dados e suas chaves de criptografia de banco de dados associadas, execute a seguinte instrução:  
  
```  
  
SELECT * FROM sys.dm_database_encryption_keys;   
GO  
  
```  
  
 Para instruções de Transact-SQL de informações detalhadas que foram usadas nesta lição, consulte [criar banco de dados &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql), [ALTER DATABASE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql), [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql), [criar certificado &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql), e [sys.dm_database_ encryption_keys &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql).  
  
 **Próxima lição:**  
  
 [Lição 6: Migrar um banco de dados de uma fonte de máquina local a uma máquina de destino no Windows Azure](lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
