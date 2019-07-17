---
title: Definir atribuições e outros comandos de Script | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a96f96319c76c9c4d5a9b22a6e613ed8bf90cee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178824"
---
# <a name="define-assignments-and-other-script-commands"></a>Definir atribuições e outros comandos de script
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Para criar um script vazio, no Designer de Cubo, na guia **Cálculos** , clique no ícone **Novo ScriptCommand** na barra de ferramentas. Quando você criar um novo script, inicialmente, ele será exibido com um título em branco no painel **Organizador de Script** da guia Cálculos. Os caracteres que você digitar no painel Expressões de Cálculo serão visíveis como o nome do item no **Organizador de Script**. Portanto, convém digitar um nome comentado na primeira linha para facilitar a identificação do script no painel **Organizador de Script** . Para obter mais informações, consulte [Introdução ao script MDX no Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892).  
  
> [!IMPORTANT]  
>  Quando você inicialmente muda para a guia **Cálculos** do Designer de Cubo, o painel **Organizador de Script** contém um único script com um comando CALCULATE. O comando CALCULATE controla a agregação das células do cubo e deve ser editado somente se você pretender especificar manualmente como o cubo será agregado.  
  
 Você pode usar o painel Expressões de Cálculo para construir uma expressão em sintaxe MDX. Ao criar a expressão, você pode copiar ou arrastar os componentes, funções e modelos do cubo do painel **Ferramentas de Cálculo** para o painel Expressões de Cálculo. Isso adicionará o script do item ao painel Expressões de Cálculo no local para onde você o arrastar ou copiar. Substitua os argumentos e seus delimitadores (« e ») pelos valores apropriados.  
  
> [!IMPORTANT]  
>  Ao gravar uma expressão que contém várias instruções usando o painel Expressões de Cálculo, certifique-se de que todas as linhas do script MDX, exceto a última, terminam com um ponto-e-vírgula (;). Os cálculos são concatenados em um único script MDX e cada script possui um ponto-e-vírgula anexado a ele para garantir a compilação correta do script MDX. Se você adicionar um ponto-e-vírgula à última linha do script no painel Expressões de Cálculo, o cubo será construído e implantado corretamente, mas não será possível executar consultas nele.  
  
## <a name="see-also"></a>Consulte também  
 [Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
