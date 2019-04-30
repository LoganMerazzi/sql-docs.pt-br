---
title: Funções definidas pelo usuário e procedimentos armazenados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a91e1e45be22ade9e7eeb7358bb83c4875f6b0b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63059449"
---
# <a name="user-defined-functions-and-stored-procedures"></a>Funções e procedimentos armazenados definidos pelo usuário
  Com os objetos de servidor do ADOMD.NET, você pode criar a função definida pelo usuário (UDF) ou procedimentos armazenados para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que interagem com os metadados e dados do servidor. Esses métodos em processo são chamados por meio de instruções MDX (Multidimensional Expressions), DMX (Data Mining Extensions) para fornecerem funcionalidade agregada sem as latências associadas às comunicações de rede.  
  
## <a name="udf-examples"></a>Exemplos de UDF  
 Um UDF é um método que pode ser chamado no contexto de uma instrução MDX ou DMX, pode conter qualquer número de parâmetros e pode retornar qualquer tipo de dados.  
  
 Um UDF criado com MDX é semelhante a um criado para DMX. A principal diferença é que certas propriedades do objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context>, como as propriedades <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentCube%2A> e <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentMiningModel%2A>, só estão disponíveis para uma linguagem de scripts ou para a outra.  
  
 Os exemplos a seguir mostram como usar um UDF para retornar uma descrição de nó, filtrar tuplas e aplicar um filtro a uma tupla.  
  
### <a name="returning-a-node-description"></a>Retornando uma descrição de nó  
 O exemplo a seguir cria um UDF que retorna a descrição de um nó especificado. O UDF usa o contexto atual em que está sendo executado e usa uma cláusula FROM do DMX para recuperar o nó do modelo de mineração atual.  
  
```  
public string GetNodeDescription(string nodeUniqueName)  
{  
   return Context.CurrentMiningModel.GetNodeFromUniqueName(nodeUniqueName).Description;  
}  
```  
  
 Uma vez implantado, o exemplo de UDF anterior pode ser chamado pela expressão DMX a seguir, que recupera o nó de previsão mais provável. A descrição contém informações que descrevem as condições que compõem o nó de previsão.  
  
```  
select Cluster(), SampleAssembly.GetNodeDescription( PredictNodeId(Cluster()) ) FROM [Customer Clusters]  
```  
  
### <a name="returning-tuples"></a>Retornando tuplas  
 O exemplo a seguir obtém um conjunto e uma contagem de retorno e recupera tuplas do conjunto de forma aleatória, retornando um subconjunto final:  
  
```  
public Set RandomSample(Set set, int returnCount)  
{  
   //Return the original set if there are fewer tuples  
   //in the set than the number requested.  
   if (set.Tuples.Count <= returnCount)  
      return set;  
  
   System.Random r = new System.Random();  
   SetBuilder returnSet = new SetBuilder();  
  
   //Retrieve random tuples until the return set is filled.  
   int i = set.Tuples.Count;  
   foreach (Tuple t in set.Tuples)  
   {  
      if (r.Next(i) < returnCount)  
      {  
         returnCount--;  
         returnSet.Add(t);  
      }  
      i--;  
      //Stop the loop if we have enough tuples.  
      if (returnCount == 0)  
         break;  
   }  
   return returnSet.ToSet();  
}  
```  
  
 O exemplo anterior é chamado no exemplo de MDX a seguir. Neste exemplo de MDX, cinco estados ou províncias aleatórios são recuperadas do **Adventure Works** banco de dados.  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
### <a name="applying-a-filter-to-a-tuple"></a>Aplicando um filtro a uma tupla  
 No exemplo a seguir, um UDF é definido para obter um conjunto, e aplicar um filtro a cada tupla no conjunto, usando o objeto Expression. Qualquer tupla compatível com o filtro será adicionada a um conjunto retornado.  
  
 [!code-cs[Adomd.NetServer#FilterSet](../../analysis-services/multidimensional-models-adomd-net-server/codesnippet/csharp/user-defined-functions-a_1.cs)]  
  
 O exemplo anterior é chamado no exemplo de MDX a seguir, que filtra o conjunto para cidades com nomes começando com 'A'.  
  
```  
Select Measures.Members on Rows,  
SampleAssembly.FilterSet([Customer].[Customer Geography].[City], "[Customer].[Customer Geography].[City].CurrentMember.Name < 'B'") on Columns  
From [Adventure Works]  
```  
  
## <a name="stored-procedure-example"></a>Exemplo de procedimento armazenado  
 No exemplo a seguir, um procedimento armazenado baseado em MDX usa AMO para criar partições, se necessário, para Vendas na Internet.  
  
 [!code-cs[Adomd.NetServer#CreateInternetSalesMeasureGroupPartitions](../../analysis-services/multidimensional-models-adomd-net-server/codesnippet/csharp/user-defined-functions-a_2.cs)]  
  
  
