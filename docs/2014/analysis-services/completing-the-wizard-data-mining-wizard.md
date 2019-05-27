---
title: Concluindo o Assistente (Assistente de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.finish.f1
ms.assetid: 6aef1548-35eb-42fd-ae87-63650a79eda1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95b1e9822296e26a187b333140ea89c47cb05466
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66087709"
---
# <a name="completing-the-wizard-data-mining-wizard"></a>Concluindo o assistente (Assistente de Mineração de Dados)
  Use a página **Concluindo o Assistente** para revisar a estrutura de mineração que será criada quando o assistente for concluído. Você também pode definir o nome da estrutura de mineração.  
  
 Se você optou por criar um modelo de mineração associado, poderá também definir o nome do modelo e habilitar o detalhamento nele.  
  
> [!NOTE]  
>  Essa página é alterada de acordo com a seleção da opção **De banco de dados relacional ou data warehouse existente** ou **De cubo existente** na página **Selecionar o Método de Definição** do assistente.  
  
 **Para obter mais informações:** [Assistente de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [Designer de mineração de dados](data-mining/data-mining-designer.md), [criar uma estrutura de mineração relacional](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opções  
 **Nome da estrutura de mineração**  
 Digite o nome da estrutura de mineração definido pelo **Assistente de Mineração de Dados**.  
  
 **Nome do modelo de mineração**  
 Digite o nome do modelo de mineração definido pelo **Assistente de Mineração de Dados**.  
  
 **Permitir detalhamento**  
 Selecione para oferecer suporte a capacidades de detalhamento no modelo de mineração novo, se tiver criado um.  
  
> [!NOTE]  
>  O detalhamento na estrutura de mineração está habilitado por padrão.  
  
 Para obter mais informações sobre opções de detalhamento, consulte [Consultas de detalhamento  40Mineração de dados 41](data-mining/drillthrough-queries-data-mining.md).  
  
 **Visualização**  
 Exibe a estrutura de mineração a ser criada.  
  
 **Criar dimensão do modelo de mineração**  
 Selecione para criar uma dimensão com base no modelo de mineração a ser criado. Depois de selecionar essa opção, digite o nome da dimensão a ser criado. Essa opção ativará a opção **Criar cubo usando a dimensão do modelo de mineração**.  
  
> [!NOTE]  
>  Essa opção ficará disponível se você selecionar **De cubo existente** na página **Selecionar o Método de Definição** do assistente.  
  
 **Criar cubo usando a dimensão do modelo de mineração**  
 Selecione para criar um cubo com base no modelo de mineração a ser criado. Depois de selecionar essa opção, digite o nome do cubo a ser criado.  
  
> [!NOTE]  
>  Essa opção ficará disponível se você selecionar a opção **De cubo existente** na página **Selecionar o Método de Definição** e tiver selecionado **Criar Dimensão de Modelo de Mineração** na página atual do assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Selecionar exibição da fonte de dados &#40;Assistente de mineração de dados&#41;](select-data-source-view-data-mining-wizard.md)   
 [Especificar os dados de treinamento &#40;Assistente de mineração de dados&#41;](specify-the-training-data-data-mining-wizard.md)  
  
  
