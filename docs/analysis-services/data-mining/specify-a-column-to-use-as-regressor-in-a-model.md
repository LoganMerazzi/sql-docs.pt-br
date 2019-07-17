---
title: Especifique uma coluna para usar como Regressor em um modelo | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0cfbe8f17c14518b2acf41bdb9ecf64b1679ffb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68182347"
---
# <a name="specify-a-column-to-use-as-regressor-in-a-model"></a>Especificar uma coluna para usar como regressor em um modelo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um modelo de regressão linear representa o valor do atributo previsível como resultado de uma fórmula, que combina as entradas de forma que os dados são ajustados o mais próximo possível a uma linha de regressão estimada. O algoritmo aceita somente valores numéricos como entradas e detecta automaticamente as entradas que oferecem o melhor ajuste.  
  
 Entretanto, você poderá especificar que uma coluna seja incluída como um regressor adicionando o parâmetro FORCE_REGRESSOR ao modelo e especificando os regressores a serem usados. Você poderá fazer isso nos casos em que o atributo tenha significado, mesmo se o efeito for muito pequeno para ser detectado pelo modelo, ou quando quiser assegurar que o atributo seja incluído na fórmula.  
  
 O procedimento a seguir descreve como criar um modelo de regressão linear simples, usando os mesmos dados de exemplo que são usados para o [tutorial de redes neurais](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b). O modelo não é necessariamente robusto, mas demonstra como usar o Designer de Mineração de Dados para personalizar um modelo de regressão linear.  
  
### <a name="how-to-create-a-simple-linear-regression-model"></a>Como criar um modelo de regressão linear simples  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no **Gerenciador de Soluções**, expanda **Estruturas de Mineração**.  
  
2.  Clique duas vezes em Call Center.dmm para abri-lo no designer.  
  
3.  No menu **Modelo de Mineração** , selecione **Novo Modelo de Mineração**.  
  
4.  Para o algoritmo, selecione **Regressão Linear da Microsoft**. Para o nome, digite **Regressão de Call Center**.  
  
5.  Na guia **Modelos de Mineração** , altere o uso de colunas como a seguir. Todas as colunas que não estiverem na lista a seguir deverão ser definidas como **Ignorar**, caso ainda não estejam.  
  
     FactCallCenterID**Key**  
  
     ServiceGrade**PredictOnly**  
  
     Total de operadores**Entrada**  
  
     AverageTimePerIssue**Input**  
  
6.  No menu **Modelo de Mineração** , selecione **Definir Parâmetros do Modelo**.  
  
7.  Para o parâmetro FORCE_REGRESSOR, na coluna **Valor** , digite os nomes de colunas entre colchetes e separados por uma vírgula, como a seguir:  
  
    ```  
    [Average Time Per Issue],[Total Operators]  
    ```  
  
    > [!NOTE]  
    >  O algoritmo detectará automaticamente que colunas são os melhores regressores. Você precisará apenas impor os regressores quando desejar assegurar que uma coluna seja incluída na fórmula final.  
  
8.  No menu **Modelo de Mineração** , selecione **Processar Modelo**.  
  
     No visualizador, o modelo é representando como um único nó contendo a fórmula de regressão. Você poderá exibir a fórmula na **Legenda de Mineração**ou extrair os coeficientes da fórmula usando consultas.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo Regressão Linear da Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)   
 [Referência Técnica do Algoritmo de Regressão Linear da Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
