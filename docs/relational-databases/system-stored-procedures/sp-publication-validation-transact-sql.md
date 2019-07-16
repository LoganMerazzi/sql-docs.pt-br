---
title: sp_publication_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: stevestein
ms.author: sstein
ms.openlocfilehash: c7e6323c8a20aec7d464f7aa6f11a27fc24728d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896617"
---
# <a name="sppublicationvalidation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia uma solicitação de validação de artigo para cada artigo na publicação especificada. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication=** ] **'** _publicação '_  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [ **@rowcount_only=** ] *rowcount_only*  
 Especifica se apenas a contagem de linhas da tabela deve ser retornada. *rowcount_only* está **smallint** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Execute uma soma de verificação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 compatível.<br /><br /> Observação: Quando um artigo for filtrado horizontalmente, uma operação de contagem de linhas é executada em vez de uma operação de soma de verificação.|  
|**1** (padrão)|Só execute uma verificação de número de linhas.|  
|**2**|Execute uma verificação de número de linhas e soma de verificação binária.<br /><br /> Observação: Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes versão 7.0, só uma validação de número de linhas é executada.|  
  
 [ **@full_or_fast=** ] *full_or_fast*  
 É o método usado para calcular a contagem de linhas. *full_or_fast* está **tinyint** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Efetua contagem completa usando COUNT (*).|  
|**1**|Efetua contagem rápida de **sysindexes**. Contagem de linhas em [sys. sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) é muito mais rápido do que contar linhas na tabela atual. No entanto, porque [sys. sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) é lentamente atualizado, o número de linhas pode não ser preciso.|  
|**2** (padrão)|Efetua contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, um COUNT(*) completo sempre será usado.|  
  
`[ @shutdown_agent = ] shutdown_agent` É se o Distribution Agent deve desligado imediatamente após a conclusão da validação. *shutdown_agent* está **bit**, com um padrão de **0**. Se **0**, o agente de replicação não desligará. Se **1**, o agente de replicação desligará após o último artigo é validado.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado ao solicitar uma validação em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_publication_validation** é usado em replicação transacional.  
  
 **sp_publication_validation** pode ser chamado a qualquer momento depois que os artigos associados com a publicação tem sido ativados. O procedimento pode ser executado manualmente (uma vez) ou como parte de um trabalho agendado regularmente que valida a data.  
  
 Se seu aplicativo tiver assinantes de atualização imediata **sp_publication_validation** poderá detectar erros falsos. **sp_publication_validation** primeiro calcula o número de linhas ou a soma de verificação no publicador e, em seguida, no assinante. Como o gatilho de atualização imediata pode propagar e atualizar do Assinante para o Publicador após a conclusão do número de linhas ou da soma de verificação no Publicador, mas antes que o número de linhas ou a soma de verificação estejam concluídos no Assinante, os valores podem alterar. Para garantir que os valores no Assinante e no Publicador não sejam alterados durante a validação de uma publicação, pare o serviço MS DTC (Coordenador de Transações Distribuídas da Microsoft) no Publicador durante a validação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_publication_validation**.  
  
## <a name="see-also"></a>Consulte também  
 [Validar dados no assinante](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
