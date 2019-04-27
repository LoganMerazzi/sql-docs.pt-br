---
title: Guia características (Visualizador do modelo de mineração) do atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.characteristics.f1
ms.assetid: f0c3350d-84c0-4ab8-9fb8-1527c2647299
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 724ac86a4566bac4647e8e7358608c0f5e4ccd85
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650707"
---
# <a name="attribute-characteristics-tab-mining-model-viewer"></a>Guia Características de Atributo (Visualizador do Modelo de Mineração)
  Use o painel **Características do Atributo** para explorar as relações entre resultados e atributos de entrada em um modelo de Naïve Bayes. Você pode escolher o valor do atributo de destino e, em seguida, ver uma lista de atributos de entrada que tiverem o efeito mais forte nos resultados.  
  
 **Para obter mais informações:** [Algoritmo Microsoft Naive Bayes](data-mining/microsoft-naive-bayes-algorithm.md), [procurar um modelo usando o visualizador Microsoft Naive Bayes](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração a ser exibido, dos modelos na estrutura de mineração atual. O modelo de mineração abrirá automaticamente em um visualizador personalizado que seja melhor para o tipo específico de modelo você escolheu.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Para cada modelo, você tem a escolha de um visualizador personalizado ou o Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Os visualizadores de plug-in também serão exibidos, se houver.  
  
 **Atributo**  
 Escolha o atributo previsível que você deseja analisar.  
  
 **Value**  
 Escolha um estado para os atributos previsíveis definidos em **Atributo**. Como os modelos de Naïve Bayes não dão suporte a variáveis contínuas, todos os atributos de destino têm resultados discretos ou diferenciados. O atributo Ausente sempre é adicionado automaticamente à lista.  
  
 **Características para \<estado previsível >**  
 O gráfico contém as seguintes colunas, que descrevem como os estados dos atributos de entrada estão relacionados ao estado do atributo previsível.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Variável**|Lista os atributos de entrada no modelo de mineração.|  
|**Valores**|Lista cada estado do atributo de entrada em **Variáveis**.|  
|**Probabilidade**|A barra representa a probabilidade de que o atributo e o valor na linha estejam associados ao estado selecionado a partir do atributo previsível. Passe o mouse sobre a barra para exibir a probabilidade como um percentual.|  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  
