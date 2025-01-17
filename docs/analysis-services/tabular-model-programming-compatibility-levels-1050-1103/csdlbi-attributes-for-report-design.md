---
title: Atributos CSDLBI para Design de relatórios | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c7f4b1ef3b46e4564ffc4622b39e8326adf443a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163460"
---
# <a name="csdlbi-attributes-for-report-design"></a>Atributos CSDLBI para design de relatórios
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Esta seção descreve os atributos nas extensões de CSDL para modelagem de tabela que afeta o design de consulta [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
## <a name="model-attributes"></a>Atributos de Modelo  
 Estes atributos são definidos em um subelemento de um elemento [EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx) de CSDL.  
  
|Nome do atributo|Tipo de dados|Descrição|  
|--------------------|---------------|-----------------|  
|Cultura|Text|Indica a cultura usada para formatos de conversor de moedas. Se for omitido, pt-BR será usado.|  
|IsRightToLeft|Boolean|Indica se os valores de campos de texto devem ser lidos da direita para a esquerda por padrão|  
  
## <a name="entity-attributes"></a>Atributos da entidade  
 Estes atributos são definidos em um subelemento de um elemento EntitySet ou EntityType de CSDL.  
  
|Nome do atributo|Tipo de dados|Descrição|  
|--------------------|---------------|-----------------|  
|**Nome da referência**|Text|O identificador usado para referenciar essa entidade em uma consulta DAX. Se for omitido, o nome será usado.|  
|**Caption**|Text|O nome para exibição da entidade.|  
|**Documentação**|Text|Texto descritivo para ajudar os usuários empresariais a compreenderem o significado dos dados.|  
|**Oculto**|Boolean|Indica se a entidade deve ser exibida. O padrão é **false**.|  
|**CollectionCaption**|Text|Nome plural para referenciar um conjunto de instâncias da entidade. Se ele for omitido, o atributo Caption será usado.|  
|**DisplayKey**|MemberRef[]|Uma lista ordenada de campo(s) usada para identificar uma instância de entidade para um usuário empresarial. As referências podem incluir propriedades de instância e propriedades de navegação. Quando uma propriedade de navegação é referenciada, o **DisplayKey** da entidade de destino é exibido. Se o valor **DisplayKey** for omitido, o campo de chave será usado.|  
|**DefaultImage**|MemberRef|Uma referência ao campo que contém uma imagem usada para identificar visualmente uma instância de entidade para um usuário empresarial. Se for omitida, o primeiro campo de imagem na entidade será usado, caso exista.|  
|**DefaultDetails**|MemberRef[]|Uma lista ordenada de campos que representam o conjunto padrão de informações detalhadas exibidas para um usuário comercial sobre uma instância de entidade. Caso sejam omitidos, serão usados os primeiros cinco (5) campos na entidade, excluindo os já referenciados por **Key**, **DisplayKey**ou **DefaultImage**.|  
|**SortProperties**|MemberRef[]|Uma lista ordenada de campos através dos quais as instâncias de entidade costumam ser classificadas. Ao classificar nestes campos, o **SortDirection** especificado em cada campo é usado. Se ele for omitido, os campos **DisplayKey** serão usados|  
|**DefaultMeasure**|MemberRef|Uma referência a uma medida definida no modelo, ou a um campo numérico com uma função de agregação padrão, para indicar que a medida ou o campo dever ser usado como a representação padrão para várias instâncias da entidade. Se ela for omitida, uma contagem das instâncias de entidade será usada.|  
|**DefaultLocation**|MemberRef|Uma referência a um campo cujo valor representa a localização padrão associada a uma instância de entidade. Se ela for omitida, o primeiro campo de localização na entidade será usado, caso exista.|  
  
## <a name="field-attributes"></a>Atributos de campo  
 Estes atributos são definidos em um subelemento de uma propriedade CSDL ou elemento [NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx) .  
  
|Nome do atributo|Tipo de dados|Descrição|  
|--------------------|---------------|-----------------|  
|**Nome da referência**|Text|O identificador usado para referenciar essa entidade em uma consulta DAX. Se ele for omitido, o nome do campo será usado.|  
|**Caption**|Text|O nome para exibição da entidade. Se omitido, o campo **ReferenceName** é usado.|  
|**Documentação**|Text|Texto descritivo para ajudar os usuários empresariais a compreenderem o significado do campo.|  
|**Oculto**|Boolean|Indica se o campo deve ser exibido. O padrão é **false**; isso significa que o campo é exibido.|  
|**DisplayFolder**|Text|O nome (caminho completo) da pasta na qual este campo é exibido. Se ele for omitido, o campo será exibido na raiz do modelo.|  
|**ContextualNameRule**|Enum|Um valor que indica se e como o nome da propriedade deve ser modificado com base no contexto no qual é usado. Os valores possíveis são:  **None**, **função**, **Merge**.|  
|**Alinhamento**|Enum|Um valor que indica como os valores de campos devem ser alinhados em uma apresentação de tabela. Os valores possíveis são **Default**, **Center**, **Left**, **Right**. Se omitido, o padrão determina o alinhamento com base no tipo de dados do campo.|  
|**FormatString**|Text|Uma cadeia de formato .NET que indica como o valor do campo deve ser formatado por padrão. Se for omitida, o seguinte formato será assumido:<br /><br /> Campos - Datetime: data curta regional ou "d"<br /><br /> -Função de agregação de campos ponto flutuante e integral com um padrão: número regional ou "n"<br /><br /> -Função de agregação inteiros sem nenhum padrão: número decimal regional ou "d"<br /><br /> Para todos os outros tipos de campos, nenhuma cadeia de caracteres de formato se aplica.|  
|**Unidades**|Text|O símbolo que se aplica a valores de campos para expressar unidades. Se ele for omitido, as unidades são consideradas desconhecidas.|  
|**Width**|Inteiro|A largura preferencial em caracteres que deve ser reservado para exibir os valores do campo em uma apresentação de tabela. Se omitido, uma largura padrão se baseia no tipo de dados do campo.|  
|**SortDirection**|Enum|Um valor que indica como os valores de campos costumam ser classificados. Os valores possíveis são **Default**, **Ascending**, **Descending**. Se omitido, o valor padrão atribuirá que uma direção de classificação baseia-se nos dados do campo de tipo.|  
|**IsRightToLeft**|Boolean|Indica se o campo contém texto que deve ser lido da direita para a esquerda. Se ele for omitido, a configuração do modelo será assumida.|  
|**OrderBy**|MemberRef|Uma referência a outro campo dentro do modelo que define a ordem de classificação para valores desse campo. Os valores para os dois campos devem ter um mapeamento 1:1 ou o comportamento de classificação será indefinido. Se ela for omitida, o campo será classificado com base em seu próprio valor.|  
|**Conteúdo**|Enum|Uma enumeração que descreve o subtipo ou o conteúdo do campo. Se omitido, Nenhum subtipo específico será considerado, a menos que o tipo de dados do campo seja Binary, caso em que Image será assumido. Para obter uma lista completa dos tipos de conteúdo com suporte, consulte a documentação de AMO.|  
|**DefaultAggregateFunction**|Enum|Um valor que indica a função padrão, caso exista, que costuma ser usada para agregar este campo. Os valores possíveis são **None**, **Sum**, **Average**, **Count**, **Min**, **Max**. Se ele for omitido, **Sum** será assumido para campos numéricos e **None** para todos os outros campos.|  
|**IsSimpleMeasure**|Boolean|Indica se uma medida é meramente uma agregação simples de um campo numérico. Estas agregações podem ser definidas facilmente na consulta quando necessário e, portanto, devem ser omitidas da definição modelo para melhorar o desempenho. Se ela for omitida, **false** será assumido.|  
|**KPI**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|Subelemento|Indica que o elemento de medida será usado como um KPI. O subelemento de KPI usa os elementos KpiGoal e KpiStauts para definir a imagem de exibição associada e os intervalos de destino.|  
  
  
