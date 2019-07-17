---
title: Propriedades de dimensão de banco de dados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7c7944ab279f2b036a3acd7cf75bd775d0ec6d6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68180779"
---
# <a name="database-dimension-properties"></a>Propriedades de dimensão do banco de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], as características de uma dimensão são definidas pelos metadados da dimensão, com base nas configurações de várias propriedades de dimensão e nos atributos ou hierarquias contidas pela dimensão. A tabela a seguir descreve as propriedades de dimensão no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**AttributeAllMemberName**|Especifica o nome de todos os membros para atributos em uma dimensão.|  
|**Ordenação**|Determina a ordenação usada pela dimensão.|  
|**CurrentStorageMode**|Contém o modo de armazenamento atual para a dimensão.|  
|**DependsOnDimension**|Contém o ID de outra dimensão da qual a dimensão depende, se houver.|  
|**Descrição**|Contém a descrição da dimensão.|  
|**ErrorConfiguration**|Contém definições configuráveis de tratamento de erros para tratamento de chaves duplicadas, chaves desconhecidas, limites de erro, ação devido à detecção de erros, arquivo de log de erros e tratamento de chaves nulas.|  
|**ID**|Contém o identificador exclusivo (ID) da dimensão.|  
|**Idioma**|Especifica o idioma padrão para a dimensão.|  
|**MdxMissingMemberMode**|Determina como são tratados membros ausentes para linguagens MDX.|  
|**MiningModelID**|Contém o ID do modelo de mineração com o qual a dimensão de mineração de dados está associada. Essa propriedade só será aplicável se a dimensão for uma dimensão de modelo de mineração.|  
|**Name**|Especifica o nome da dimensão.|  
|**ProactiveCaching**|Define configurações de cache pró-ativas para a dimensão.|  
|**ProcessingGroup**|Especifica o grupo de processamento. Os valores são ByAttribute ou ByTable. O padrão é **ByAttribute**.|  
|**ProcessingMode**|Indica se o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve fazer indexação e agregação durante ou após o processamento.|  
|**ProcessingPriority**|Determina a prioridade de processamento da dimensão durante as operações em segundo plano, como agregações lentas, indexação ou cluster.|  
|**Source**|Identifica a exibição da fonte de dados à qual a dimensão está associada.|  
|**StorageMode**|Determina o modo de armazenamento da dimensão.|  
|**Tipo**|Especifica o tipo da dimensão.|  
|**UnknownMember**|Indica se o membro desconhecido é visível.|  
|**UnknownMemberName**|Especifica a legenda, no idioma padrão da dimensão, para o membro desconhecido da dimensão.|  
|**WriteEnabled**|Indica se write-backs de dimensão estão disponíveis (sujeito a permissões de segurança).|  
  
> [!NOTE]  
>  Para obter mais informações sobre como definir valores para as propriedades ErrorConfiguration e UnknownMember quando trabalhar com valores nulos e outros problemas de integridade de dados, consulte [Handling Data Integrity Issues in Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Hierarquias do usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Relações de dimensão](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
