---
title: Elemento Create (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Create element (DTA)
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3541a007b51d5813a6bc42a977ec31fedf5bab87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104991"
---
# <a name="create-element-dta"></a>Criar elemento (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Contém informações sobre estruturas de índices, estatísticas e de heap em uma configuração especificada pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Necessária uma vez para cada tipo de estrutura física de design (estruturas de índices, estatísticas ou de heap).|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Recommendation &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)|  
|**Elementos filho**|[Elemento Index &#40;DTA&#41;](../../tools/dta/index-element-dta.md)<br /><br /> Elemento**Statistics** (veja o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://schemas.microsoft.com/sqlserver/) para obter informações)<br /><br /> Elemento**Heap** (veja o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://schemas.microsoft.com/sqlserver/) para obter informações)|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento tem o nome **CreateTypecomplexType** no esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. É usado criar estruturas de índices, estatísticas e de heap em uma configuração especificada pelo usuário. Não confunda esse elemento **Create** com os outros tipos que podem ser usados para criar exibições (**CreateViewType**) ou particionamento (**CreatePType**). Consulte o [esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](https://schemas.microsoft.com/sqlserver/) para obter informações sobre esses outros tipos de elementos **Create** .  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
