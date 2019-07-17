---
title: Suporte a FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47ea988c3c9ec2b784109e46ce30d1a0ed56dc61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987519"
---
# <a name="filestream-support"></a>Suporte a FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  FILESTREAM é uma forma de armazenar e acessar valores altos de binário, por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou por acesso direto ao sistema de arquivos do Windows. Um valor binário grande é um valor superior a 2 gigabytes (GB). Para obter mais informações sobre suporte a FILESTREAM aprimorado, consulte [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
 Quando uma conexão de banco de dados for aberta, **@@TEXTSIZE** será definido, por padrão, como -1 ("ilimitado").  
  
 Também é possível acessar e atualizar colunas FILESTREAM usando as APIs do sistema de arquivos do Windows.  
  
 Para mais informações, consulte os seguintes tópicos:  
  
-   [Suporte a FILESTREAM &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [Suporte a FILESTREAM &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [Acessar dados do FILESTREAM com OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Consultando colunas FILESTREAM  
 Conjuntos de linhas de esquema no OLE DB não relatarão se uma coluna é uma coluna FILESTREAM. ITableDefinition no OLE DB não pode ser usado para criar uma coluna FILESTREAM.  
  
 Funções de catálogo como SQLColumns no ODBC não relatarão se uma coluna é uma coluna FILESTREAM.  
  
 Para criar colunas FILESTREAM ou detectar quais colunas existentes são colunas FILESTREAM, use a coluna **is_filestream** da exibição de catálogo [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).  
  
 A seguir, é mostrado um exemplo:  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Compatibilidade com níveis inferiores  
 Se seu cliente tiver sido compilado usando a versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que foi incluído [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], e o aplicativo se conecta ao [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], **varbinary (max)** comportamento serão compatível com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Ou seja, o tamanho máximo de dados retornados será limitado a 2 GB. Para valores de resultado superiores a 2 GB, ocorrerá truncamento e será retornado um aviso de "truncamento à direita de dados de cadeia de caracteres".  
  
 Quando a compatibilidade de tipo de dados estiver definida como 80, o comportamento do cliente será consistente com o comportamento de clientes de nível inferior.  
  
 Para clientes que usam SQLOLEDB ou outros provedores lançados antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, **varbinary (max)** será mapeado para imagem.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
