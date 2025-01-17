---
title: sysschemaarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysschemaarticles_TSQL
- sysschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysschemaarticles system table
ms.assetid: 67a1c039-c283-4a9c-bacc-b9b3973590c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 594c984be10d592246696730dd393efdfc48e259
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029601"
---
# <a name="sysschemaarticles-transact-sql"></a>sysschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Controla artigos somente esquema para publicações transacional e de instantâneo. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|A ID do artigo.|  
|**creation_script**|**nvarchar(255)**|O caminho e o nome de um script de esquema de artigo usados para criar a tabela de destino.|  
|**description**|**nvarchar(255)**|A entrada descritiva para o artigo.|  
|**dest_object**|**sysname**|O nome do objeto no banco de dados de assinatura, se o artigo for um artigo somente esquema como um procedimento armazenado, uma exibição ou UDF.|  
|**name**|**sysname**|O nome do artigo somente esquema em uma publicação.|  
|**objid**|**int**|O identificador de objeto do objeto base do artigo. Pode ser o identificador de objeto de um procedimento, exibição indexada, exibição ou UDF.|  
|**pubid**|**int**|A ID da publicação.|  
|**pre_creation_cmd**|**tinyint**|Especifica o que o sistema deve fazer se detectar um objeto existente com o mesmo nome no Assinante, ao aplicar o instantâneo para esse artigo:<br /><br /> **0** = nothing.<br /><br /> **1** = excluir tabela de destino.<br /><br /> **2** = tabela de destino de soltar.<br /><br /> **3** = tabela de destino de truncamento.|  
|**status**|**int**|O bitmap usado para indicar o status do artigo.|  
|**type**|**tinyint**|O valor que indica o tipo de artigo somente esquema:<br /><br /> **32** = procedimento armazenado.<br /><br /> **64** = exibição ou exibição indexada. <br /><br /> **96** = função de agregação.<br /><br /> **128** = função.|  
|**schema_option**|**binary(8)**|O bitmask da opção de geração de esquema para o artigo determinado. Especifica criação automática de procedimento armazenado no banco de dados de destino para todas as sintaxes CALL/MCALL/XCALL, e pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **0x00** = desabilita execução de script pelo Snapshot Agent e usa *creation_script*.<br /><br /> **0x01** = gera a criação do objeto (CREATE TABLE, CREATE PROCEDURE e assim por diante). Esse valor é o padrão para artigos de procedimento armazenado.<br /><br /> **0x02** = gera procedimentos armazenados personalizados para o artigo, se definido.<br /><br /> **0x10** = gera um índice clusterizado correspondente.<br /><br /> **0x20** = converte tipos de dados definidos pelo usuário para tipos de dados base.<br /><br /> **0x40**= gera índices não clusterizados correspondentes.<br /><br /> **0x80**= inclui integridade referencial declarada nas chaves primárias.<br /><br /> **0x73** = gera a instrução CREATE TABLE, cria índices clusterizados e não clusterizados, converte tipos de dados definidos pelo usuário para tipos de dados base e gera scripts de procedimento armazenado personalizado a ser aplicado no assinante. Esse valor é o padrão para todos os artigos, exceto os de procedimento armazenado.<br /><br /> **0x100**= replica gatilhos de usuário em um artigo de tabela, se definido.<br /><br /> **0x200**= replica restrições de chave estrangeiras. Se a tabela referenciada não fizer parte de uma publicação, todas as restrições de chave estrangeira em uma tabela publicada não serão replicadas.<br /><br /> **0x400**= replica restrições de verificação.<br /><br /> **0x800**= replica padrões.<br /><br /> **0x1000**= replica agrupamento em nível de coluna.<br /><br /> **0x2000**= replica propriedades estendidas associadas com o objeto de origem do artigo publicado.<br /><br /> **0x4000**= replica chaves exclusivas definidas em um artigo de tabela.<br /><br /> **0x8000**= replica chave primária e chaves exclusivas em um artigo de tabela como restrições usando instruções ALTER TABLE.|  
|**dest_owner**|**sysname**|O proprietário da tabela no banco de dados de destino.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
