---
title: Gerenciar alterações em exibições da fonte de dados e fontes de dados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f8cb72fe4650cd76465207f3e7cd529e2a7b032
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208814"
---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>Gerenciar alterações em exibições da fonte de dados e em fontes de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando o Assistente de Geração de Esquema é executado novamente, ele reutiliza a fonte de dados e a exibição da fonte de dados usadas na geração original. Se você adicionar uma fonte de dados ou uma exibição da fonte de dados, o assistente não a usará. Se você excluir a fonte de dados ou a exibição da fonte de dados original depois da geração inicial, execute o assistente desde o início. Também são excluídas todas as configurações anteriores do assistente. Todos os objetos existentes em um banco de dados subjacente que estavam vinculados a uma fonte de dados ou exibição de fonte de dados excluída serão tratados como objetos criados pelo usuário na próxima vez que você executar o Assistente de Geração de Esquema.  
  
 Se a exibição da fonte de dados não refletir o estado real do banco de dados subjacente no momento da geração, o Assistente de Geração de Esquema pode encontrar erros ao gerar o esquema para o banco de dados da área de assunto. Por exemplo, se a exibição da fonte de dados especificar que o tipo de dados de uma coluna é **int**, mas, na verdade, o tipo de dados da coluna for **string**, o Assistente de Geração de Esquema definirá o tipo de dados da chave estrangeira como **INT** de acordo com a exibição da fonte de dados e, em seguida, não conseguirá criar a relação, pois o tipo de dados real é **string**.  
  
 Por outro lado, se você alterar a cadeia de conexão da fonte de dados para um banco de dados diferente daquele usado na geração anterior, nenhum erro será gerado. O novo banco de dados será usado e nenhuma alteração será feita no banco de dados anterior.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre a geração com incremento](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)  
  
  
