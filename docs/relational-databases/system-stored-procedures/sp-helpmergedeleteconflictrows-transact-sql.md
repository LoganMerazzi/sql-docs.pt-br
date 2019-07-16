---
title: sp_helpmergedeleteconflictrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergedeleteconflictrows
- sp_helpmergedeleteconflictrows_TSQL
helpviewer_keywords:
- sp_helpmergedeleteconflictrows
ms.assetid: 222be651-5690-4341-9dfb-f9ec1d80c970
author: stevestein
ms.author: sstein
ms.openlocfilehash: 86e8d3d21246cbb308db5b698a29f2b02ce45ac3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137746"
---
# <a name="sphelpmergedeleteconflictrows-transact-sql"></a>sp_helpmergedeleteconflictrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre linhas de dados perdedoras no conflito de exclusão. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Assinante, no banco de dados de assinatura, quando um logon de conflito descentralizado é usado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergedeleteconflictrows [ [ @publication = ] 'publication']  
    [ , [ @source_object = ] 'source_object']  
    [ , [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publsher_db'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, com um padrão de **%** . Se a publicação for especificada, serão retornados todos os conflitos qualificados pela publicação.  
  
`[ @source_object = ] 'source_object'` É o nome do objeto de origem. *source_object* está **nvarchar(386)** , com um padrão NULL.  
  
`[ @publisher = ] 'publisher'` É o nome do publicador. *publisher* é **sysname**, com um padrão NULL.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicador. *publisher_db* é **sysname**, com um padrão NULL.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**source_object**|**nvarchar(386)**|Objeto de origem para o conflito de exclusão.|  
|**rowguid**|**uniqueidentifier**|Identificador de linha para o conflito de exclusão.|  
|**conflict_type**|**int**|Código que indica tipo de conflito:<br /><br /> **1** = UpdateConflict: Conflito é detectado no nível de linha.<br /><br /> **2** = ColumnUpdateConflict: Conflito detectado no nível de coluna.<br /><br /> **3** = UpdateDeleteWinsConflict: Exclusão ganha o conflito.<br /><br /> **4** = UpdateWinsDeleteConflict: O rowguid excluído que perde o conflito é registrado nessa tabela.<br /><br /> **5** = UploadInsertFailed: Inserção do assinante não pôde ser aplicada no publicador.<br /><br /> **6** = DownloadInsertFailed: Inserção do publicador não pôde ser aplicada no assinante.<br /><br /> **7** = UploadDeleteFailed: Exclusão no assinante não pôde ser carregada no publicador.<br /><br /> **8** = DownloadDeleteFailed: Exclusão no publicador não pôde ser baixada no assinante.<br /><br /> **9** = UploadUpdateFailed: Atualização do assinante não puderam ser aplicada no publicador.<br /><br /> **10** = DownloadUpdateFailed: Atualização do publicador não puderam ser aplicada ao assinante.|  
|**reason_code**|**Int**|Código de erro que pode ser sensível ao contexto.|  
|**reason_text**|**varchar(720)**|Descrição de erro que pode ser sensível ao contexto.|  
|**origin_datasource**|**varchar(255)**|Origem do conflito.|  
|**pubid**|**uniqueidentifier**|Identificador da publicação.|  
|**MSrepl_create_time**|**datetime**|Hora em que as informações de conflitos foram adicionadas.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergedeleteconflictrows** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa e a **db_owner** banco de dados fixa podem executar **sp_helpmergedeleteconflictrows**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
