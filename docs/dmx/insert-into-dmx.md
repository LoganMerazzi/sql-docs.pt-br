---
title: INSERT INTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 16732c1d889f7125d71d01bd0804b4202daceb7e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62505161"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Processa o objeto de mineração de dados especificado. Para obter mais informações sobre como processar modelos de mineração e estruturas de mineração, consulte [considerações e requisitos de processamento de &#40;mineração de dados&#41;](../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Se uma estrutura de mineração for especificada, a instrução processará a estrutura de mineração e todos seus modelos de mineração associados. Se o modelo de mineração for especificado, a instrução processará apenas o modelo de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>Argumentos  
 *modelo*  
 Identificador de modelo.  
  
 *estrutura*  
 Identificador de estrutura.  
  
 *colunas de modelo mapeado*  
 Lista separada por vírgula de identificadores de coluna e identificadores aninhados.  
  
 *consulta de fonte de dados*  
 Consulta da fonte no formato definido pelo provedor.  
  
## <a name="remarks"></a>Comentários  
 Se você não especificar **modelo de MINERAÇÃO** ou **estrutura de MINERAÇÃO**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] procura o tipo de objeto com base no nome e processa o objeto correto. Se o servidor contiver uma estrutura de mineração e um modelo de mineração com nomes idênticos, um erro será retornado.  
  
 Usando a segunda forma de sintaxe, INSERT INTO*\<objeto >*. COLUMN_VALUES, você pode inserir dados diretamente nas colunas de modelo, sem treinar o modelo. Esse método fornece dados de coluna para o modelo de forma concisa, ordenada, que é útil quando se trabalha com conjuntos de dados contendo hierarquias ou colunas ordenadas.  
  
 Se você usar **INSERT INTO** com um modelo de mineração ou uma estrutura de mineração e saia desativar o \<mapear colunas do modelo > e \<consulta de fonte de dados > argumentos, a instrução se comporta como  **ProcessDefault**, usando associações já existentes. Se não houver associações, a instrução retornará um erro. Para obter mais informações sobre **ProcessDefault**, consulte [processando opções e configurações &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md). O exemplo a seguir mostra a sintaxe:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Se você especificar **modelo de MINERAÇÃO** e forneça colunas mapeadas e uma consulta de fonte de dados, o modelo e estrutura associada é processado.  
  
 A tabela a seguir fornece uma descrição do resultado de diferentes formas de instruções, dependendo do estado dos objetos.  
  
|de|Estado de objetos|Resultado|  
|---------------|----------------------|------------|  
|INSERT INTO MINING MODEL*\<modelo >*|A estrutura de mineração é processada.|O modelo de mineração é processado.|  
||A estrutura de mineração é não processada.|O modelo de mineração e a estrutura de mineração são processadas.|  
||A estrutura de mineração contém modelos de mineração adicionais.|Falha no processo. É preciso reprocessar a estrutura e os modelos de mineração associados.|  
|INSERT INTO MINING STRUCTURE*\<estrutura >*|A estrutura de mineração é processada ou não processada.|A estrutura de mineração e os modelos de mineração associados são processados.|  
|INSERT INTO MINING MODEL*\<modelo >* que contém uma consulta de origem<br /><br /> ou em<br /><br /> INSERT INTO MINING STRUCTURE*\<estrutura >* que contém uma consulta de origem|A estrutura ou o modelo já encerram um conteúdo.|Falha no processo. Você deve limpar os objetos antes de executar essa operação, usando [excluir &#40;DMX&#41;](../dmx/delete-dmx.md).|  
  
## <a name="mapped-model-columns"></a>Colunas de modelo mapeado  
 Usando o \<mapear colunas do modelo > elemento, você pode mapear as colunas da fonte de dados para as colunas no modelo de mineração. O \<mapear colunas do modelo > elemento tem o seguinte formato:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Usando **SKIP**, você pode excluir determinadas colunas que devem existir na consulta de fonte, mas que não existem no modelo de mineração. SKIP é útil quando você não tem controle sobre as colunas que estão incluídas no conjunto de linhas de entrada. Se você estiver escrevendo sua própria OPENQUERY, a prática recomendada é omitir a coluna da lista de colunas SELECT em vez de usar SKIP.  
  
 SKIP também é útil quando uma coluna do conjunto de linhas de entrada é necessária para executar uma junção, mas a coluna não é usada pela estrutura de mineração. Um exemplo típico disso é uma estrutura de mineração e modelo de mineração que contêm uma tabela aninhada. O conjunto de linhas de entrada desta estrutura terá uma coluna de chave estrangeira usada para criar um conjunto de linhas hierárquico usando a cláusula SHAPE, mas a coluna de chave estrangeira quase nunca é usada no modelo.  
  
 A sintaxe de SKIP requer que você insira SKIP na posição da coluna individual no conjunto de linhas de entrada que não tem nenhuma coluna de estrutura de mineração correspondente. Por exemplo, na tabela aninhada a seguir, OrderNumber deve ser selecionado na cláusula APPEND para que possa ser usado na cláusula RELATE para especificar a junção. No entanto, você não precisa inserir os dados de OrderNumber na tabela aninhada na estrutura de mineração. Portanto o exemplo usa a palavra-chave SKIP em vez de OrderNumber no argumento INSERT INTO.  
  
## <a name="source-data-query"></a>Consulta de dados de origem  
 O \<consulta de dados de origem > elemento pode incluir os seguintes tipos de fonte de dados:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **FORMA**  
  
-   Qualquer consulta [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que retorne um conjunto de linhas  
  
 Para obter mais informações sobre tipos de fonte de dados, consulte [ &#60;consulta de fonte de dados&#62;](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Exemplo básico  
 O exemplo a seguir usa **OPENQUERY** para treinar um modelo Naive Bayes com base em dados de endereçamento de destino no [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] banco de dados.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>Exemplo de tabela aninhada  
 O exemplo a seguir usa **forma** para treinar um modelo de mineração de associação que contém uma tabela aninhada. Observe que a primeira linha contém **SKIP** em vez disso, OrderNumber que é necessária a **SHAPE_APPEND** instrução, mas não é usado no modelo de mineração.  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
