---
title: Ferramentas de cálculo (guia Ações, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionsview.calculationtoolspane.f1
ms.assetid: a3370370-43cd-4cc2-bb9f-c0d988b96f05
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 087f5f5e3383fd66244541fea35160946936bc1c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088342"
---
# <a name="calculation-tools-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Ferramentas de Cálculo (guia Ações, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Ferramentas de Cálculo** da guia **Ações** no Designer de Cubo para explorar metadados, funções e modelos disponíveis para uso em ações, ações de extração de detalhes e ações de relatório.  
  
## <a name="options"></a>Opções  
 **Metadados**  
 Exibe os metadados do cubo selecionado.  
  
 Arraste um elemento selecionado para o painel **Action Form Editor (Editor de Formulário de Ação)**, **Drillthrough Action Form Editor (Editor de Formulário de Ação de Extração de Detalhes)** ou **Report Action Form Editor (Editor de Formulário de Ação de Relatório)** para incluir a sintaxe MDX (Multidimensional Expressions) daquele elemento no local selecionado no painel.  
  
 **Funções**  
 Exibe as funções disponíveis para expressões e condições.  
  
 Arraste um elemento selecionado para o painel **Editor de Formulário de Ação**, **Editor de Formulário de Ação de Extração de Detalhes**ou **Editor de Formulário de Ação de Relatório** para incluir a sintaxe MDX daquele elemento no local selecionado no painel.  
  
> [!NOTE]  
>  No modo de projeto, a caixa de diálogo **Ferramentas de Cálculo** lê as informações desta opção em um arquivo XML denominado MDXFunctions.xml fornecido com o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Em modo online, informações para esta opção são recuperadas do conjunto de linhas de esquema de MDSCHEMA_FUNCTIONS da instância.  
  
 **Modelos**  
 Exibe os modelos predefinidos disponíveis para ações.  
  
 Arraste um elemento selecionado para o painel **Editor de Formulário de Ação**, **Editor de Formulário de Ação de Extração de Detalhes**ou **Editor de Formulário de Ação de Relatório** para incluir a sintaxe MDX daquele elemento no local selecionado no painel.  
  
## <a name="context-menu"></a>Menu de contexto  
 As seguintes opções estão disponíveis no menu de contexto exibido ao clicar com o botão direito do mouse em um elemento exibido no painel **Ferramentas de Cálculo** :  
  
|Opção|Definição|  
|------------|----------------|  
|**Copiar**|Selecione para copiar o elemento selecionado em **Metadados** ou **Funções** na Área de Transferência.<br /><br /> Observe que essa opção não será exibida se **modelos** está selecionado. Observe também que essa opção será desabilitada se não puder do membro selecionado ser copiado, como o **conjuntos** pasta de uma dimensão exibida em **metadados** ou a pasta do grupo de funções de uma função exibida em  **Funções**.|  
|**Filtrar membros**|Clique para exibir a caixa de diálogo **Filtrar Membros** e filtrar os membros exibidos para o elemento selecionado em **Metadados**. Para obter mais informações sobre a caixa de diálogo **Filtrar Membros**, consulte [Caixa de diálogo Filtrar Membros &#40;Analysis Services – Dados Multidimensionais&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Observe que essa opção é exibida somente se **metadados** está selecionado. Observe também que essa opção é habilitada somente se um nível de um atributo é selecionado na **metadados**.|  
|**Adicionar modelo**|Selecione para adicionar uma nova ação, ação de extração de detalhes ou ação de relatório com base no modelo selecionado ao cubo e exibir, respectivamente, o **Editor de Formulário de Ação**, **Editor de Formulário de Ação de Extração de Detalhes**ou **Editor de Formulário de Ação de Relatório**.<br /><br /> Observação: Esta opção será exibida apenas se a opção **Metadados** estiver selecionada.|  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do script MDX &#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Ações &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de ações &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de detalhamento &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de relatório &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
