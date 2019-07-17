---
title: Detalhar dados do caso de um modelo de mineração | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7b5b2cbfd141642cb5d36d0ec67958ec7ae14ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210054"
---
# <a name="drill-through-to-case-data-from-a-mining-model"></a>Detalhar dados do caso a partir do modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se um modelo de mineração foi configurado para permitir que você detalhe os casos de modelo, quando você procurar o modelo, poderá recuperar informações detalhadas sobre os casos usados para criar o modelo. Além do mais, se a estrutura de mineração subjacente tiver sido configurada para permitir o detalhamento para casos de estrutura e você tiver as permissões adequadas, poderá retornar as informações a partir da estrutura de mineração. Isso pode incluir colunas que não foram incluídas no modelo de mineração.  
  
 Se a estrutura de mineração não permitir que você detalhe os dados subjacentes, mas o modelo de mineração permitir, você poderá exibir informações dos casos de modelo e não da estrutura de mineração.  
  
> [!NOTE]  
>  Você pode acrescentar a habilidade de detalhamento em um modelo de mineração existente, configurando a propriedade **AllowDrillthrough** para **True**. Porém, depois que você habilitar o detalhamento, o modelo deverá ser reprocessado antes que você possa ver os dados do caso. Para obter mais informações,consulte [Habilitar drillthrough para um modelo de mineração](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 Dependendo do tipo de visualizador utilizado, é possível selecionar o nó a ser detalhado das seguintes formas:  
  
|Nome do visualizador|Painel ou nome da guia|Selecionar nó|  
|-----------------|----------------------|-----------------|  
|**Visualizador de árvores da Microsoft**|Guia**Árvore de Decisão**|Clique em um nó de árvore.<br /><br /> **Observação** : Evita usar o detalhamento no nó **All** uma vez que isso pode levar muito tempo para retornar resultados.|  
|**Visualizador de cluster da Microsoft**|**Diagrama de Cluster**|Clique em um nó de cluster.|  
|**Visualizador de cluster da Microsoft**|**Perfis de Cluster**|Clique em qualquer parte da coluna de cluster.|  
|**Visualizador de Associação da Microsoft**|Guia**Regras**|Clique em uma linha que contém um conjunto de regras.|  
|**Visualizador de Associação da Microsoft**|Guia**Conjuntos de Itens**|Clique em uma linha que contém um conjunto de itens.|  
|**Visualizador de Cluster de Sequência da Microsoft**|Guia**Regras**|Clique em uma linha que contém um conjunto de regras.|  
|**Visualizador de Cluster de Sequência da Microsoft**|Guia**Conjuntos de Itens**|Clique em uma linha que contém um conjunto de itens.|  
  
> [!NOTE]  
>  Alguns modelos não podem usar detalhamento. A capacidade de usar detalhamento depende do algoritmo utilizado para criar o modelo. Para obter uma lista dos tipos de modelo de mineração que dão suporte ao drillthrough, consulte [Consultas de detalhamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Para exibir dados de detalhamento de um modelo de mineração  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra a estrutura de mineração que contém o modelo de mineração desejado.  
  
2.  No Designer de Mineração de Dados, clique na guia **Visualizador do Modelo de Mineração** .  
  
3.  Selecione o modelo na lista suspensa **Modelo de Mineração** .  
  
4.  Selecione um visualizador na lista suspensa **Visualizador** e clique com o botão direito do mouse no nó específico.  
  
5.  Selecione **Detalhar**e, em seguida, selecione **Somente Colunas de Modelos**ou **Colunas de Modelo e Estrutura** para abrir a janela **Detalhar** .  
  
6.  Para copiar os dados para a Área de Transferência, clique com o botão direito do mouse na tabela e selecione **Copiar Tudo**.  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de detalhamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
  
