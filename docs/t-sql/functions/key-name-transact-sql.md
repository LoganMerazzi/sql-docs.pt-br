---
title: KEY_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KEY_NAME_TSQL
- KEY_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- KEY_NAME function
ms.assetid: 7b693e5d-2325-4bf9-9b45-ad6a23374b41
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bd2246ed1a6c2c03e3a9f5c1989ce9e544c8b199
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109330"
---
# <a name="keyname-transact-sql"></a>KEY_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o nome da chave simétrica de um GUID de chave simétrica ou de um texto codificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
KEY_NAME ( ciphertext | key_guid )   
```  
  
## <a name="arguments"></a>Argumentos  
 *ciphertext*  
 É o texto criptografado pela chave simétrica. *cyphertext* é do tipo **varbinary(8000)** .  
  
 *key_guid*  
 É o GUID da chave simétrica. *key_guid* é do tipo **uniqueidentifier**.  
  
## <a name="returned-types"></a>Tipos retornados  
 **varchar(128)**  
  
## <a name="permissions"></a>Permissões  
 A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], a visibilidade dos metadados está limitada aos protegíveis que pertencem a um usuário ou nos quais ele tem alguma permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-the-name-of-a-symmetric-key-using-the-keyguid"></a>A. Exibindo o nome de uma chave simétrica com o uso de key_guid  
 O banco de dados **master** contém uma chave simétrica chamada ##MS_ServiceMasterKey##. O exemplo a seguir obtém o GUID dessa chave da exibição de gerenciamento dinâmico sys.symmetric_keys, o atribui a uma variável e, em seguida, passa essa variável para a função KEY_NAME para demonstrar como retornar o nome que corresponde ao GUID.  
  
```  
USE master;  
GO  
DECLARE @guid uniqueidentifier ;  
SELECT @guid = key_guid FROM sys.symmetric_keys  
WHERE name = '##MS_ServiceMasterKey##' ;  
-- Demonstration of passing a GUID to KEY_NAME to receive a name  
SELECT KEY_NAME(@guid) AS [Name of Key];  
```  
  
### <a name="b-displaying-the-name-of-a-symmetric-key-using-the-cipher-text"></a>B. Exibindo o nome de uma chave simétrica com o uso de texto codificado  
 O exemplo a seguir demonstra o processo inteiro da criação de uma chave simétrica e do preenchimento de dados em uma tabela. O exemplo mostra como KEY_NAME retorna o nome da chave quando passou o texto criptografado.  
  
```  
-- Create a symmetric key  
CREATE SYMMETRIC KEY TestSymKey   
   WITH ALGORITHM = AES_128,  
   KEY_SOURCE = 'The square of the hypotenuse is equal to the sum of the squares of the sides',  
   IDENTITY_VALUE = 'Pythagoras'  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y' ;  
GO  
-- Create a table for the demonstration  
CREATE TABLE DemoKey  
(IDCol int IDENTITY PRIMARY KEY,  
SecretCol varbinary(256) NOT NULL)  
GO  
-- Open the symmetric key if not already open  
OPEN SYMMETRIC KEY TestSymKey   
    DECRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
-- Insert a row into the DemoKey table  
DECLARE @key_GUID uniqueidentifier;  
SELECT @key_GUID = key_guid FROM sys.symmetric_keys  
WHERE name LIKE 'TestSymKey' ;  
INSERT INTO DemoKey(SecretCol)  
VALUES ( ENCRYPTBYKEY (@key_GUID, 'EncryptedText'))  
GO  
-- Verify the DemoKey data  
SELECT * FROM DemoKey;  
GO  
-- Decrypt the data  
DECLARE @ciphertext varbinary(256);  
SELECT @ciphertext = SecretCol  
FROM DemoKey WHERE IDCol = 1 ;  
SELECT CAST (  
DECRYPTBYKEY( @ciphertext)  
AS varchar(100) ) AS SecretText ;  
-- Use KEY_NAME to view the name of the key  
SELECT KEY_NAME(@ciphertext) AS [Name of Key] ;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEYAUTOASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykeyautoasymkey-transact-sql.md)  
  
  
