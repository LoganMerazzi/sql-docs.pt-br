---
title: Catalog. validations (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: dbafe110-b480-48f3-b45f-31d71ca68f62
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2d799fd23c2adef75e3dcf4543e9e0ee6271c9b5
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogvalidations-ssisdb-database"></a>catalog.validations (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os detalhes de todas as validações de projeto e pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|validation_id|**bigint**|O identificador exclusivo (ID) da validação.|  
|environment_scope|**Char (1)**|Indica as referências de ambiente que são consideradas pela validação. Quando o valor for `A`, todas as referências de ambiente associadas ao projeto serão incluídas na validação. Quando o valor for `S`, apenas uma única referência de ambiente será incluída. Quando o valor for `D`, nenhuma referência de ambiente será incluída e cada parâmetro deverá ter um valor padrão literal a fim de ser aprovado na validação.|  
|validate_type|**Char (1)**|O tipo de validação a ser executado. Os possíveis tipos de validação são validação de dependência (`D`) ou validação completa (`F`). A validação de pacote é sempre uma validação completa.|  
|nome_da_pasta|**nvarchar (128)**|O nome da pasta que contém o projeto correspondente.|  
|project_name|**nvarchar (128)**|O nome do projeto.|  
|project_lsn|**bigint**|A versão do projeto contra a qual é feita a validação.|  
|use32bitruntime|**bit**|Indica se o tempo de execução de 32 bits é usado para executar o pacote em um sistema operacional de 64 bits. Quando o valor for `1`, a execução é realizada com o tempo de execução de 32 bits. Quando o valor é `0`, a execução é realizada com o tempo de execução de 64 bits.|  
|reference_id|**bigint**|A ID exclusiva da referência de ambiente do projeto que é usada pelo projeto para fazer referência a um ambiente.|  
|operation_type|**smallint**|O tipo de operação. As operações mostradas nessa exibição incluem a validação de projeto (`300`) e a validação de pacote (`301`).|  
|object_name|**nvarhcar(260)**|O nome do objeto.|  
|object_type|**smallint**|O tipo do objeto. O objeto pode ser um projeto (`20`) ou um pacote (`30`).|  
|object_id|**bigint**|A ID do objeto afetado pela operação.|  
|start_time|**DateTimeOffset(7)**|A hora de início da operação.|  
|end_time|**datetimeoffsset(7)**|A hora em que a operação é concluída.|  
|status|**int**|O status da operação. Os possíveis valores são criado (`1`), em execução (`2`), cancelado (`3`), com falha (`4`), pendente (`5`), encerrado inesperadamente (`6`), êxito (`7`), parando (`8`) e concluído (`9`).|  
|caller_sid|**varbinary(85)**|O SID (identificador de segurança) do usuário se a Autenticação do Windows tiver sido usada para fazer logon.|  
|caller_name|**nvarchar (128)**|O nome da conta que executou a operação.|  
|process_id|**int**|A ID de processo do processo externo, se aplicável.|  
|stopped_by_sid|**varbinary(85)**|O SID do usuário que interrompeu a operação.|  
|stopped_by_name|**nvarchar (128)**|O nome do usuário que interrompeu a operação.|  
|server_name|**nvarchar (128)**|As informações do servidor e da instância do Windows de uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|machine_name|**nvarchar (128)**|O nome do computador no qual a instância de servidor está sendo executada.|  
|dump_id|**uniqueidentifier**|A ID do despejo de execução.|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição mostra uma linha para cada validação no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na operação correspondente  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  