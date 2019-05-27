---
title: Selecionar membros (Assistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.memberconversion.f1
ms.assetid: 1a147461-d594-41e7-a41d-09d2d003e1e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7cc66896eb1735d09991644dd49c03b5a94c208d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069427"
---
# <a name="select-members-business-intelligence-wizard"></a>Selecionar Membros (Assistente de Business Intelligence)
  Use a página **Selecionar Membros** para determinar a quais membros o Assistente de Business Intelligence deve aplicar a funcionalidade de conversão de moeda especificada na página **Definir Opções de Conversão de Moeda** .  
  
> [!NOTE]  
>  Essa página não será exibida se o Assistente de Business Intelligence tiver sido iniciado no Designer de Dimensão ou clicando com o botão direito do mouse em uma dimensão no Gerenciador de Soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opções  
 **Dimensão de medidas**  
 Selecione para aplicar a funcionalidade de conversão de moeda a uma ou mais medidas no cubo.  
  
 Se selecionada, a grade exibirá as opções listadas na tabela a seguir.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Tipos de medidas internas**|Selecione para incluir funcionalidade de conversão de moeda para a medida especificada.|  
|**Medidas**|Selecione a medida do grupo de medidas de taxa que contém a taxa de câmbio a ser usada ao converter a medida selecionada em **Tipos de Medidas Internas** .|  
  
 **Hierarquia de contas**  
 Selecione para aplicar a funcionalidade de conversão de moeda a um ou mais membros da hierarquia de contas da dimensão de conta incluída no cubo. A hierarquia de contas é a hierarquia dentro da conta da dimensão cuja `Type` estiver definida como *conta*.  
  
 Se selecionada, a grade exibirá as opções listadas na tabela a seguir.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Membro da conta**|Selecione para incluir funcionalidade de conversão de moeda para o membro especificado da hierarquia de contas.|  
|**Medidas**|Selecione a medida do grupo de medidas de taxa que contém a taxa de câmbio a ser usada quando as medidas do membro selecionado em **Membro da Conta** forem convertidas.|  
  
 **Com base no tipo de hierarquia de contas**  
 Selecione para aplicar a funcionalidade de conversão de moeda a todos os membros de atributos na hierarquia de contas cuja propriedade `Type` está definida como um tipo de conta especificado.  
  
 Se selecionada, a grade exibirá as opções listadas na tabela a seguir.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Tipo de conta**|Selecione para incluir funcionalidade de conversão de moeda para o tipo de conta especificado.|  
|**Medidas**|Selecione a medida do grupo de medidas de taxa que contém a taxa de câmbio a ser usada ao converter medidas para os membros de atributos usando o tipo de conta selecionado em **Tipo de Conta** .|  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Designer de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Designer de dimensão &#40;Analysis Services - dados multidimensionais&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
