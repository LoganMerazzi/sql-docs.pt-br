---
title: DM filestream_non_transacted_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_non_transacted_handles_TSQL
- dm_filestream_non_transacted_handles
- dm_filestream_non_transacted_handles_TSQL
- sys.dm_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_non_transacted_handles dynamic management view
ms.assetid: 507ec125-67dc-450a-9081-94cde5444a92
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4dda607ace977be539dbed096a3d83ac5f220ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950989"
---
# <a name="sysdmfilestreamnontransactedhandles-transact-sql"></a>sys.dm_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe os identificadores de arquivos não transacionais abertos atualmente associados aos dados da FileTable.  
  
 Essa exibição contém uma linha por identificador de arquivo aberto. Como os dados dessa exibição correspondem ao estado interno ativo do servidor, os dados são alterados constantemente conforme os identificadores são abertos e fechados. Essa exibição não contém informações de histórico.  
  
 Para obter mais informações, consulte [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md).  
  
|**Coluna**|**Tipo**|**Descrição**|  
|----------------|--------------|---------------------|  
|database_id|int|ID do banco de dados associado ao identificador.|  
|object_id|int|ID do objeto da FileTable à qual o identificador está associado.|  
|handle_id|int|Identificador de contexto de identificador exclusivo. Usado pelas [sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md) procedimento armazenado para eliminar um identificador específico.|  
|file_object_type|int|O tipo do identificador. Indica o nível da hierarquia na qual o identificador foi aberto, ou seja, o banco de dados ou o item.|  
|file_object_type_desc|nvarchar(120)|"UNDEFINED",<br />"SERVER_ROOT",<br />"DATABASE_ROOT",<br />"TABLE_ROOT",<br />"TABLE_ITEM"|  
|correlation_process_id|varbinary(8)|Contém um identificador exclusivo para o processo que originou a solicitação.|  
|correlation_thread_id|varbinary(8)|Contém um identificador exclusivo para o thread que originou a solicitação.|  
|file_context|varbinary(8)|Ponteiro para o objeto de arquivo usado por este identificador.|  
|state|int|O estado atual do identificador. Pode ser ativo, fechado ou eliminado.|  
|state_desc|nvarchar(120)|"ATIVO",<br />"FECHADO",<br />"INTERROMPIDA"|  
|current_workitem_type|int|Estado pelo qual este identificador está sendo processado.|  
|current_workitem_type_desc|nvarchar(120)|"NoSetWorkItemType",<br />"FFtPreCreateWorkitem",<br />"FFtGetPhysicalFileNameWorkitem",<br />"FFtPostCreateWorkitem",<br />"FFtPreCleanupWorkitem",<br />"FFtPostCleanupWorkitem",<br />"FFtPreCloseWorkitem",<br />"FFtQueryDirectoryWorkItem",<br />"FFtQueryInfoWorkItem",<br />"FFtQueryVolumeInfoWorkItem",<br />"FFtSetInfoWorkitem",<br />"FFtWriteCompletionWorkitem"|  
|fcb_id|BIGINT|ID do bloco de controle de arquivo da FileTable.|  
|item_id|varbinary(892)|A ID do item de um arquivo ou diretório. Pode ser nulo para identificadores de raiz de servidor.|  
|is_directory|bit|Este é um diretório.|  
|item_name|nvarchar(512)|Nome do item.|  
|opened_file_name|nvarchar(512)|Caminho originalmente solicitado para ser aberto.|  
|database_directory_name|nvarchar(512)|Parte do opened_file_name que representa o nome do diretório do banco de dados.|  
|table_directory_name|nvarchar(512)|Parte do opened_file_name que representa o nome do diretório da tabela.|  
|remaining_file_name|nvarchar(512)|Parte do opened_file_name que representa o nome do diretório restante.|  
|open_time|datetime|Hora em que o identificador foi aberto.|  
|sinalizadores|int|ShareFlagsUpdatedToFcb = 0x1,<br />DeleteOnClose = 0x2,<br />NewFile = 0x4,<br />PostCreateDoneForNewFile = 0x8,<br />StreamFileOverwritten = 0x10,<br />RequestCancelled = 0x20,<br />NewFileCreationRolledBack = 0x40|  
|login_id|int|ID da entidade de segurança que abriu o identificador.|  
|login_name|nvarchar(512)|Nome da entidade de segurança que abriu o identificador.|  
|login_sid|varbinary(85)|SID da entidade de segurança que abriu o identificador.|  
|read_access|bit|Aberto para acesso de leitura.|  
|write_access|bit|Aberto para acesso de gravação.|  
|delete_access|bit|Aberto para acesso de exclusão.|  
|share_read|bit|Aberto com share_read permitido.|  
|share_write|bit|Aberto com share_write permitido.|  
|share_delete|bit|Aberto com share_delete permitido.|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
