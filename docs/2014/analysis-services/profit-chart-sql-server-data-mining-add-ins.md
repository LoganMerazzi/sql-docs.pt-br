---
title: (SQL Server Data Mining Add-ins) do gráfico de ganho | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- profit chart
- mining models, charting
- mining models, testing
ms.assetid: 5c902543-4da9-4db3-99d5-4ce04c43d7ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ddeafaafd816e226edff764c8e273cde6df4eaad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748450"
---
# <a name="profit-chart-sql-server-data-mining-add-ins"></a>Gráfico de Ganho (Suplementos de Mineração de Dados do SQL Server)
  ![Botão gráfico de ganho na faixa de opções mineração de dados](media/dmc-profitchart.gif "botão gráfico de ganho na faixa de opções mineração de dados")  
  
 Um gráfico de ganho exibe o aumento estimado de lucro associado ao uso de um modelo de mineração para determinar quais clientes uma empresa deve contatar em um cenário comercial. O eixo Y do gráfico representa o ganho, enquanto que o eixo X representa a porcentagem da população que a empresa contatou. Um gráfico de ganho típico mostra um aumento nos lucros até certo ponto; depois disso, os lucros diminuem à medida que mais pessoas são contatadas.  
  
## <a name="configuring-the-profit-chart"></a>Configurando o gráfico de ganho  
 Enquanto o gráfico de precisão avalia apenas a probabilidade de as previsões estarem certas ou erradas, o gráfico de ganho incorpora conhecimentos reais sobre as consequências de executar uma ação em uma previsão. Isso é obtido considerando-se os seguintes fatores, que você especifica ao executar o assistente:  
  
-   **População**  
  
     O número de casos no conjunto de dados que está sendo usado para criar o gráfico de comparação de precisão. Por exemplo, o número de clientes em potencial.  
  
-   **Custo Fixo**  
  
     O custo fixo associado ao problema empresarial. Caso seja destinado a uma solução de correspondência de destino, o custo não poderá depender de variáveis como o número de chamadas telefônicas feitas ou o número de correspondências promocionais enviadas.  
  
-   **Custo Individual**  
  
     Os custos adicionais ao custo fixo, que podem estar associados a cada contato de cliente. Por exemplo, correspondências promocionais ou chamadas telefônicas.  
  
-   **Receita por Indivíduo**  
  
     A receita associada a cada venda bem sucedida.  
  
## <a name="using-the-profit-chart-wizard"></a>Usando o Assistente de Gráfico de Ganho  
 Para criar um gráfico de ganho, você deve referenciar um modelo de mineração de dados existente. Você pode procurar modelos para encontrar um modelo que corresponda aos dados clicando **gerenciar modelos** ou **procurar** para ver detalhes sobre o algoritmo que foi usada e as colunas no modelo de mineração.  
  
 Para obter mais informações, consulte [procurando modelos no Excel &#40;SQL Server Data Mining Add-ins&#41; ](browsing-models-in-excel-sql-server-data-mining-add-ins.md) e [gerenciar modelos &#40;SQL Server Data Mining Add-ins&#41;](manage-models-sql-server-data-mining-add-ins.md).  
  
#### <a name="to-create-a-profit-chart"></a>Para criar um gráfico de ganho  
  
1.  Selecione um modelo existente.  
  
2.  Especifique a coluna que você deseja prever e um valor de destino, se apropriado.  
  
3.  Selecione os dados de origem, o que significa que os dados passarão pelo modelo para criar uma previsão. Esses não devem ser os mesmos dados usados para criação do modelo.  
  
4.  Mapeie as colunas na nova data (origem) para as colunas usadas no modelo de mineração de dados. Se os nomes das colunas forem semelhantes, eles serão mapeados automaticamente pelo assistente.  
  
5.  Insira as informações de custo necessárias para o assistente: o custo fixo, o custo individual, a população e a receita esperada.  
  
6.  Opcionalmente, você pode inserir uma série graduada de custos (clique no botão Procurar **(...)**  botão). Por exemplo, talvez uma correspondência fique mais barata à medida que você aumentar o número de itens enviados, para que possa inserir um custo diferente de acordo com o número de itens, e o assistente ajustará automaticamente os custos para cada tamanho de amostra.  
  
7.  O assistente cria um gráfico que contém a análise de custo-benefício do modelo.  
  
### <a name="requirements"></a>Requisitos  
 Se você estiver prevendo um valor numérico discreto, selecione o valor de destino exato para prever.  
  
## <a name="understanding-the-profit-chart"></a>Entendendo o gráfico de ganho  
 O gráfico de ganho contém uma linha vertical cinza, que você pode mover clicando em um local do gráfico. O **legenda de mineração** exibe uma pontuação, a correção da população e a probabilidade de previsão que estão associados com o local da linha cinza no gráfico. Se você selecionar o ponto máximo de lucros no gráfico usando a linha cinza, utilize o valor de probabilidade de previsão para determinar um limite de probabilidade para contatar um cliente.  
  
 Por exemplo, se o ponto máximo da curva de lucro estiver em 55% da população e a probabilidade de previsão associada for 20%, isso indica que para alcançar o máximo de lucro, você só deve contatar os clientes cuja resposta esteja prevista com uma probabilidade de 20% ou mais.  
  
## <a name="see-also"></a>Consulte também  
 [Validando modelos e usando modelos para previsão &#40;Data Mining Add-ins para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
