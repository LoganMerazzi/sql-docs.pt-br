---
title: Escolha a coluna para usar para testar um modelo de mineração | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bcfe927f3b58787ab316a637d0c1d493f73c104a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62725170"
---
# <a name="choose-the-column-to-use-for-testing-a-mining-model"></a>Escolha a coluna para usar para teste em um modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Antes de poder medir a exatidão de um modelo de mineração, você deverá decidir qual resultado deseja avaliar. A maioria dos modelos de mineração de dados exige que você escolha pelo menos uma coluna para usar como o atributo previsível ao criar o modelo. Portanto, quando você testar a exatidão do modelo, geralmente terá que selecionar esse atributo para testar.  
  
 A lista a seguir descreve algumas considerações adicionais para escolher o atributo previsível para usar no teste:  
  
-   Alguns tipos de modelos de mineração de dados podem prever vários atributos, como redes neurais, que podem explorar as relações entre muitos atributos.  
  
-   Outros tipos de mineração, modelos, como modelos de clustering-não necessariamente não tem um atributo previsível. Os modelos de clustering não podem ser testados a menos que tenham um atributo previsível.  
  
-   Criar um gráfico de dispersão ou medir a exatidão de um modelo de regressão exige que você escolha um atributo previsível contínuo como o resultado. Nesse caso, você não pode especificar um valor de destino. Se você estiver criando algo diferente de um gráfico de dispersão, a coluna da estrutura de mineração subjacente também terá que ter um tipo de conteúdo **Discreto** ou **Discretizado**.  
  
-   Se você escolher um atributo discreto como o resultado previsível, também poderá especificar um valor de destino ou pode deixar em branco o campo **Valor de Previsão** . Se você incluir um **valor de previsão**, o gráfico medirá somente a efetividade do modelo ao prever o valor de destino. Se você não especificar um resultado de destino, o modelo será medido para sua exatidão em prever todos os resultados.  
  
-   Se você quiser incluir diversos modelos e compará-los em um único gráfico de precisão, todos os modelos deverão usar a mesma coluna previsível.  
  
-   Quando você cria um relatório de validação cruzada, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] automaticamente analisa todos os modelos que têm o mesmo atributo previsível.  
  
-   Quando a opção **Sincronizar Colunas e Valores de Previsão**é selecionada, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] automaticamente escolhe as colunas previsíveis que têm os mesmos nomes e tipos de dados correspondentes. Se suas colunas não atenderem a estes critérios, você poderá desativar esta opção e manualmente escolher uma coluna previsível. Você pode precisar fazer isto se estiver testando o modelo com um conjunto de dados externo que tem colunas diferentes do modelo. Porém, se você escolher uma coluna com o tipo de dados incorreto, obterá um erro ou resultados incorretos.  
  
### <a name="specify-the-outcome-to-predict"></a>Especifique o resultado para prever  
  
1.  Clique duas vezes na estrutura de mineração para abri-la no Designer de Mineração de Dados.  
  
2.  Selecione a guia **Gráfico de Precisão de Mineração** .  
  
3.  Selecione a guia **Seleção de Entrada** .  
  
4.  Na guia **Seleção de Entrada** , em **Nome da Coluna Previsível**, selecione uma coluna previsível para cada modelo que você incluir no gráfico.  
  
     As colunas do modelo de mineração disponíveis na caixa **Nome da Coluna Previsível** são somente as que têm o tipo de uso definido como **Previsão** ou **Somente Previsão**.  
  
5.  Se quiser determinar o nível de elevação para um modelo, selecione um valor de resultado específico para medir, escolhendo na lista **Valor de Previsão** .  
  
## <a name="see-also"></a>Consulte também  
 [Escolher e mapear dados de testes modelo](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [Escolher um tipo de gráfico de precisão e definir opções de gráfico](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
