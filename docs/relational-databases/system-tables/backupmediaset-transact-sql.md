---
title: backupmediaset (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1dbaf429acb94334540f0e147eae2808e1655309
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119352"
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada conjunto de mídias de backup. Essa tabela é armazenada na **msdb** banco de dados.  
 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Número exclusivo de identificação do conjunto de mídias. Identidade, chave primária.|  
|**media_uuid**|**uniqueidentifier**|O UUID do conjunto de mídias. Todos os [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de mídia têm um UUID.<br /><br /> Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no entanto, se um conjunto de mídias contém apenas uma família de mídias, o **media_uuid** coluna pode ser NULL (**media_family_count** é 1).|  
|**media_family_count**|**tinyint**|Número de famílias de mídias no conjunto de mídias. Pode ser NULL.|  
|**name**|**nvarchar(128)**|Nome do conjunto de mídias. Pode ser NULL.<br /><br /> Para obter mais informações, consulte MEDIANAME e MEDIADESCRIPTION em [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).|  
|**description**|**nvarchar(255)**|Descrição textual do conjunto de mídias. Pode ser NULL.<br /><br /> Para obter mais informações, consulte MEDIANAME e MEDIADESCRIPTION em [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).|  
|**software_name**|**nvarchar(128)**|Nome do software de backup que gravou o rótulo da mídia. Pode ser NULL.|  
|**software_vendor_id**|**int**|Número de identificação do fornecedor de software que gravou o rótulo de backup da mídia. Pode ser NULL.<br /><br /> O valor para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é 0x1200 hexadecimal.|  
|**MTF_major_version**|**tinyint**|Número de versão principal do formato de fita do [!INCLUDE[msCoName](../../includes/msconame-md.md)] usado para gerar este conjunto de mídias. Pode ser NULL.|  
|**mirror_count**|**tinyint**|Número de espelhos no conjunto de mídias.|  
|**is_password_protected**|**bit**|É o conjunto de mídias protegido por senha:<br /><br /> 0 = Não protegido<br /><br /> 1 = Protegido|  
|**is_compressed**|**bit**|Se o backup é compactado:<br /><br /> 0 = Não compactado<br /><br /> 1 = Compactado<br /><br /> Durante um **msdb** atualização, esse valor é definido como NULL. o que indica um backup não compactado.|  
|**is_encrypted**|**Bit**|Se o backup for criptografado:<br /><br /> 0 = não criptografado<br /><br /> 1 = Criptografado|  
  
## <a name="remarks"></a>Comentários  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY preenche as colunas da **backupmediaset** tabela com os valores apropriados do cabeçalho de conjunto de mídias.  
  
 Para reduzir o número de linhas nessa tabela e em outras tabelas de histórico e backup, execute as [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
