---
title: Desenvolver tipos específicos de componentes de Script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4737f7723f7403d823ca950557bcccd41c7a750a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020068"
---
# <a name="developing-specific-types-of-script-components"></a>Desenvolvendo tipos específicos de componentes Script
  O componente de Script é uma ferramenta configurável que pode ser usada no fluxo de dados de um pacote para atender a quase todos os requisitos não atendidos pelas fontes, transformações e destinos incluídos no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Esta seção contém exemplos de código do componente Script que demonstram as quatro opções para configurar o componente Script:  
  
-   Como uma origem.  
  
-   Como uma transformação com saídas síncronas.  
  
-   Como uma transformação com saídas assíncronas.  
  
-   Como um destino.  
  
 Para obter exemplos adicionais do componente Script, consulte [Exemplos de componentes Script adicionais](../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criar uma origem com o componente de Script](creating-a-source-with-the-script-component.md)  
 Explica e demonstra como criar uma origem de fluxo de dados com o componente de Script.  
  
 [Criar uma transformação síncrona com o componente de Script](creating-a-synchronous-transformation-with-the-script-component.md)  
 Explica e demonstra como criar uma transformação de fluxo de dados com saídas síncronas usando o componente Script. Esse tipo de transformação modifica linhas de dados no local à medida que passam pelo componente.  
  
 [Criar uma transformação assíncrona com o componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 Explica e demonstra como criar uma transformação de fluxo de dados com saídas assíncronas usando o componente Script. Esse tipo de transformação tem que ler todas as linhas de dados antes de adicionar mais informações, como agregações calculadas, aos dados que passam pelo componente.  
  
 [Criar um destino com o componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 Explica e demonstra como criar um destino de fluxo de dados com o componente de Script.  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**permanecer acima para data com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Comparar soluções de script e objetos personalizados](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Desenvolvendo tipos específicos de componentes de fluxo de dados](../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  