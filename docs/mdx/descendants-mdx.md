---
title: Descendentes (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 013b7a7a2124788f3f1bcaa6d09b8ef7b10562e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248114"
---
# <a name="descendants-mdx"></a>Descendants (MDX)


  Retorna o conjunto de descendentes de um membro em uma distância ou nível especificado, incluindo ou excluindo, opcionalmente, descendentes em outros níveis.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member expression syntax using a level expression  
Descendants(Member_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Member_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
Set expression syntax using a level expression  
Descendants(Set_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Set_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *distância*  
 Uma expressão numérica válida que especifica a distância do membro especificado.  
  
 *Desc_Flag*  
 Uma expressão de cadeia de caracteres válida que especifica um sinalizador de descrição que distingue entre possíveis conjuntos de descendentes.  
  
## <a name="remarks"></a>Comentários  
 Se um nível for especificado, o **descendentes** retorna um conjunto que contém descendentes do membro especificado ou os membros do conjunto especificado em um nível especificado, opcionalmente modificado por um sinalizador especificado em  *Desc_Flag*.  
  
 Se *distância* for especificado, o **descendentes** função retorna um conjunto que contém descendentes do membro especificado ou membros do conjunto especificado que são o número especificado de níveis de distância no a hierarquia do membro especificado, opcionalmente modificado por um sinalizador especificado em *Desc_Flag*. Normalmente, você usa esta função com o argumento Distance para lidar com hierarquias com rotas. Se a distância especificada for zero (0), a função retornará um conjunto composto apenas pelo membro especificado ou pelo conjunto especificado.  
  
 Se uma expressão de conjunto for especificada, o **descendentes** função é resolvida individualmente para cada membro do conjunto, e o conjunto é criado novamente. Em outras palavras, a sintaxe usada para o **descendentes** função é funcionalmente equivalente à MDX [gerar](../mdx/generate-mdx.md) função.  
  
 Se nenhum nível ou distância for especificada, o valor padrão para o nível usado pela função é determinado por meio da chamada a [nível](../mdx/level-mdx.md) função (<\<membro >>. Nível) para o membro especificado (se um membro for especificado) ou chamando o **nível** de função para cada membro do conjunto especificado (se um conjunto é especificado). Se nenhuma expressão de nível, distância ou sinalizadores forem especificados, a função será executada como se a sintaxe seguinte fosse usada:  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Member_Expression.Level ,`  
  
 `SELF_BEFORE_AFTER`  
  
 `)`  
  
 Se um nível for especificado e um sinalizador de descrição não for, a função será executada como se a sintaxe seguinte fosse usada.  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Level_Expression,`  
  
 `SELF`  
  
 `)`  
  
 Alterando o valor do sinalizador de descrição, você pode incluir ou excluir descendentes no nível ou na distância especificada, o filho antes ou depois de um nível ou distância especificada (até o nó folha), e a folha filha, independentemente do nível ou da distância especificada. A tabela a seguir descreve os sinalizadores permitidos na *Desc_Flag* argumento.  
  
|Sinalizador|Descrição|  
|----------|-----------------|  
|SELF|Só retorna membros descendentes do nível especificado ou à distância especificada. A função inclui o membro especificado, se o nível especificado for o nível do membro especificado.|  
|AFTER|Retorna os membros descendentes de todos os níveis subordinados ao nível especificado ou à distância.|  
|BEFORE|Retorna membros descendentes de todos os níveis entre o membro especificado e o nível especificado ou à distância especificada. Inclui o membro especificado, mas não inclui membros do nível especificado ou distância.|  
|BEFORE_AND_AFTER|Retorna membros descendentes de todos os níveis subordinados ao nível do membro especificado. Inclui o membro especificado, mas não inclui membros do nível especificado ou à distância especificada.|  
|SELF_AND_AFTER|Retorna membros descendentes do nível especificado ou à distância especificada e todos os níveis subordinados ao nível especificado ou à distância especificada.|  
|SELF_AND_BEFORE|Retorna membros descendentes do nível especificado ou à distância especificada e de todos os níveis entre o membro especificado e o nível especificado ou à distância especificada, incluindo o membro especificado.|  
|SELF_BEFORE_AFTER|Retorna membros descendentes de todos os níveis subordinados ao nível do membro especificado e inclui o membro especificado.|  
|LEAVES|Retorna membros descendentes de folha entre o membro especificado e o nível especificado ou à distância especificada.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o membro especificado (Estados Unidos) e os membros entre o membro especificado (Estados Unidos) e os membros do nível anterior ao nível especificado (Cidade). O exemplo retorna o próprio membro especificado (Estados Unidos) e os membros do nível Estado-Província (o nível antes do nível Cidade). Esse exemplo inclui argumentos comentados para permitir que você teste outros argumentos facilmente para essa função.  
  
```  
SELECT Descendants  
   ([Geography].[Geography].[Country].&[United States]  
      //, [Geography].[Geography].[Country]  
   , [Geography].[Geography].[City]  
      //, [Geography].[Geography].Levels (3)  
      //, SELF   
      //, AFTER  
      , BEFORE  
      // BEFORE_AND_AFTER  
      //, SELF_AND_AFTER  
      //, SELF_AND_BEFORE  
      //,SELF_BEFORE_AFTER  
      //,LEAVES   
   ) ON 0  
FROM [Adventure Works]   
```  
  
 O exemplo a seguir retorna a média diária do `Measures.[Gross Profit Margin]` medida, calculada nos dias de cada mês do ano fiscal de 2003, a partir de **Adventure Works** cubo. O **descendentes** função retorna um conjunto de dias determinado do membro atual do `[Date].[Fiscal]` hierarquia.  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS Avg  
   (  
      Descendants( [Date].[Fiscal].CurrentMember,   
           [Date].[Fiscal].[Date]  
          ),   
        Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
   [Date].[Fiscal].[Month].Members ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Fiscal Year].&[2003])  
```  
  
 O exemplo a seguir usa uma expressão de nível e retorna o Valor de Vendas pela Internet para cada Estado-Província da Austrália, e retorna a porcentagem do total do Valor de Vendas pala Internet para a Austrália para cada Estado-Província. Este exemplo usa a função Item para extrair a primeira (e única) tupla do conjunto retornado pela **ancestrais** função.  
  
```  
WITH MEMBER Measures.x AS   
   [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],  
      Ancestors   
         ( [Customer].[Customer Geography].CurrentMember,   
           [Customer].[Customer Geography].[Country]  
         ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],   
     [Customer].[Customer Geography].[State-Province], SELF   
   )    
} ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
