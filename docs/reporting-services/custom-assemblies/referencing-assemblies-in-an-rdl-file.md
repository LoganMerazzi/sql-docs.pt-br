---
title: Referenciando assemblies em um arquivo RDL | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 87285bffd5136c4ac2a66ae17755edcecd35f065
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193976"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>Referenciando assemblies em um arquivo RDL
  Para dar suporte ao uso de assemblies de código personalizado em arquivos de definição de relatório, dois elementos da linguagem RDL foram incluídos na especificação de RDL: o elemento **CodeModules** e o elemento **Classes**.  
  
 O elemento **CodeModules** permite referenciar assemblies de código gerenciado em expressões de relatório. **CodeModules** é um elemento de nível superior que contém a referência ao assembly usado nos arquivos de definição de relatório para chamar funções especializadas. Uma entrada em uma definição de relatório que dá suporte ao uso de um assembly personalizado poderia ser assim:  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 Em vez de chamar <xref:System.Reflection.Assembly.Load%2A> do código personalizado, registre os assemblies personalizados manualmente adicionando elementos **CodeModule** ao arquivo RDL ou usando a guia **Referências** da caixa de diálogo **Propriedades do Relatório**. Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 O elemento **Classes** dá suporte ao uso de membros de instância em uma definição de relatório. **Classes** é um elemento de nível superior que contém uma referência ao nome de classe e um nome de instância. Uma entrada em uma definição de relatório que dá suporte ao uso de membros de instância poderia ser assim:  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 Para obter mais informações, consulte [Acessando assemblies personalizados por meio de expressões](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Usar assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
