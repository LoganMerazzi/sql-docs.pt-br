---
title: Criar um relatório de validação cruzada | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 88d3af205a1e92ac07a4c841c80f2abea463de9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68184110"
---
# <a name="create-a-cross-validation-report"></a>Criar um relatório de validação cruzada
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este tópico mostra passo-a-passo a criação de um relatório de validação cruzada usando a guia Gráfico de Precisão no Designer de Mineração de Dados. Para obter informações gerais sobre a aparência de um relatório de validação cruzada e as medidas estatísticas que ele inclui, consulte [Validação cruzada &#40;Analysis Services – Mineração de Dados&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).  
  
 Um relatório de validação cruzada é bem diferente de um gráfico de precisão, como um gráfico de comparação de precisão ou uma matriz de classificação.  
  
-   A validação cruzada avalia a distribuição geral de dados que são usados em um modelo ou estrutura; assim, você não especifica um conjunto de dados de teste. A validação cruzada sempre usa apenas os dados originais que foram usados para treinar o modelo ou a estrutura de mineração.  
  
-   A validação cruzada só pode ser executada em relação a um único resultado previsível. Se a estrutura oferecer suporte a modelos com atributos previsíveis diferentes, crie relatórios separados para cada saída previsível.  
  
-   Somente modelos relacionados à estrutura atual selecionada estão disponíveis para validação cruzada.  
  
-   Se a estrutura selecionada no momento der suporte a uma combinação de modelos de clustering e não clustering, quando você clicar em **Obter Resultados**, o procedimento armazenado de validação cruzada carregará automaticamente modelos que têm a mesma coluna previsível, e ignorará modelos de clustering que não compartilham o mesmo atributo previsível.  
  
-   Você pode criar um relatório de validação cruzada em um modelo de clustering que não tem um atributo previsível somente quando a estrutura de mineração não oferece suporte a outros atributos previsíveis.  
  
### <a name="select-a-mining-structure"></a>Selecionar uma estrutura de mineração  
  
1.  Abra o Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  No Gerenciador de Soluções, abra o banco de dados que contém a estrutura ou o modelo para o qual você deseja criar um relatório.  
  
3.  Clique duas vezes na estrutura de mineração para abrir a estrutura e seus modelos relacionados no Designer de Mineração de Dados.  
  
4.  Clique na guia **Gráfico de Precisão de Mineração** .  
  
5.  Clique na guia **Validação Cruzada** .  
  
### <a name="set-cross-validation-options"></a>Defina opções de validação cruzada  
  
1.  Na guia **Validação Cruzada** de **Número de Partições**, clique na seta para baixo para selecionar um número entre 1 e 10. O valor padrão é 10.  
  
     O **Número de Partições** representa o número de partições que serão criadas dentro do conjunto de dados original. Se você definir Número de Partições como 1, será usado o conjunto de treinamento sem particionamento.  
  
2.  Em **Atributo de Destino**, clique na seta para baixo e selecione uma coluna na lista. Se o modelo for um modelo de clustering, selecione **#Cluster** para indicar que o modelo não tem um atributo previsível. Note que o valor, **#Cluster**, está disponível somente quando a estrutura de mineração não oferece suporte a outros tipos de atributos previsíveis.  
  
     Você pode selecionar apenas um atributo previsível por relatório. Por padrão, todos os modelos relacionados que têm o mesmo atributo previsível são incluídos no relatório.  
  
3.  Em **Máx. de Casos**, digite um número grande o suficiente para fornecer um exemplo representativo dos dados quando eles forem divididos entre números especificados de dobras. Se o número for maior que a contagem de casos no conjunto de treinamento do modelo, todos os casos serão usados.  
  
     Se o conjunto de dados de treinamento for muito grande, a configuração do valor de **Máx. de Casos** limitará o número total de casos processados e permitirá que o relatório seja concluído mais rapidamente. Porém, você não deve definir **Máx. de Casos** como um valor muito baixo, pois pode haver dados insuficientes para validação cruzada.  
  
4.  Como opção, para **Estado de Destino**, digite o valor do atributo previsível que você quer modelar. Por exemplo, se a coluna [Bike Buyer] tiver dois valores possíveis, 1 (Sim) e 2 (Não), você poderá inserir o valor 1 para avaliar a precisão do modelo para apenas o resultado desejado.  
  
    > [!NOTE]  
    >  Se você não digitar um valor, a opção **Limite de Destino** não estará disponível e o modelo será avaliado por todos os valores possível do atributo previsível.  
  
5.  Como opção, em **Limite de Destino**, digite um número decimal entre 0 e 1 para especificar a probabilidade mínima que uma previsão deve ter para ser considerada precisa.  
  
     Para obter dicas adicionais sobre como definir limites de probabilidade, consulte [Medidas no relatório de validação cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
6.  Clique em **Obter Resultados**.  
  
### <a name="print-the-cross-validation-report"></a>Imprimir o relatório de validação cruzada  
  
1.  Clique com o botão direito do mouse no relatório completo na guia **Validação Cruzada** .  
  
2.  No menu de atalho, selecione **Imprimir** ou **Visualizar Impressão** para revisar o primeiro relatório.  
  
### <a name="create-a-copy-of-the-report-in-microsoft-excel"></a>Criar uma cópia do relatório no Microsoft Excel  
  
1.  Clique com o botão direito do mouse no relatório completo na guia **Validação Cruzada** .  
  
2.  No menu de atalho, selecione **Selecionar Tudo**.  
  
3.  Clique com o botão direito do mouse no texto selecionado e selecione **Copiar**.  
  
4.  Cole a seleção em uma pasta do Excel aberta. Se você usar a opção **Colar** , o relatório será colado no Excel como HTML, preservando a formatação de linhas e colunas. Se colar o relatório usando a opção **Colar Especial** para texto ou texto Unicode, o relatório será colado em um formato delimitado por linha.  
  
## <a name="see-also"></a>Consulte também  
 [Medidas no relatório de validação cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)  
  
  
