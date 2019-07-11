---
title: sys. resource_usage (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_usage_TSQL
- resource_usage
- sys.resource_usage
- resource_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- resource_usage
- sys.resource_usage
ms.assetid: b90147a3-fd8e-408e-961d-5c7000e068ad
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1a3a6baec134c715d5f15c0e3e45a19e17d5b5cf
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716300"
---
# <a name="sysresourceusage-azure-sql-database"></a>sys.resource_usage (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]
>  Esse recurso está em um estado de visualização. Não usa uma dependência na implementação específica desse recurso porque o recurso pode ser alterado ou removido em uma versão futura.  
> 
>  Quando está em um estado de visualização, a equipe de operações do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] pode ativar ou desativar a coleta de dados para esse DMV:  
> 
>  -   Quando ativado, o DMV retorna dados atuais à medida que são agregados.  
> -   Quando desativado, o DMV retorna os dados históricos, que podem estar obsoletos.  
  
 Fornece um resumo de hora em hora de dados de uso de recurso para bancos de dados de usuário no servidor atual. Dados históricos são retidos por 90 dias.  
  
 Para cada banco de dados de usuário, há uma linha para cada hora na forma contínua. Mesmo se o banco de dados estiver ocioso durante aquela hora, há uma linha, e o valor de usage_in_seconds para esse banco de dados será 0. O uso de armazenamento e as informações de SKU são acumuladas para a hora adequadamente.  
  
|Colunas|Tipo de dados|Descrição|  
|-------------|---------------|-----------------|  
|time|**datetime**|A hora (UTC) em incrementos de hora.|  
|database_name|**nvarchar**|Nome do banco de dados de usuário.|  
|sku|**nvarchar**|O nome da SKU. O valores possíveis são os seguintes:<br /><br /> Web<br /><br /> Business<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|Soma do tempo de CPU usado na hora.<br /><br /> Observação: Esta coluna é preterida para V11 e não se aplica à V12. **Valor é sempre definido como 0.**|  
|storage_in_megabytes|**decimal**|Tamanho máximo de armazenamento para a hora, inclusive dados do banco de dados, índices, procedimentos armazenados e metadados.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
  
