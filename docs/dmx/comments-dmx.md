---
title: Comentários (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 26a529d6eb15997ccb48ad25d8d4fcb11cd2ddfb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071050"
---
# <a name="comments-dmx"></a>Comentários (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Os comentários em extensões DMX (Data Mining) são cadeias de caracteres de texto no programa de código que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não será executada. Os comentários são também conhecidos como comentários. Os comentários são usados para documentar código ou para desabilitar temporariamente partes de um script ou instrução DMX durante o diagnóstico de um código.  
  
 Usar comentários para documentar código de programa facilita a manutenção do código no futuro. Use comentários para registrar detalhes, como o nome do programa, nome do desenvolvedor que escreveu o código e as datas de alterações significativas do código. Use igualmente os comentários para descrever cálculos complexos ou para explicar um método de programação.  
  
 A seguir, as diretrizes básicas para escrever comentários:  
  
-   É possível usar todos os caracteres alfanuméricos ou símbolos em um comentário. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora todos os caracteres constantes de um comentário.  
  
-   Não há um comprimento máximo para um comentário dentro de um script ou instrução. O comentário pode ser composto por uma ou mais linhas.  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte aos seguintes tipos de caracteres de comentário:  
  
-   **(barras duplas).** Use esses caracteres de comentário para gravar um comentário na mesma linha como código que deve ser executado, ou para gravar um comentário em uma linha por si próprio. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia tudo, desde as barras duplas até o final da linha como parte do comentário. Para criar um comentário de várias linhas, use as barras duplas no início de cada linha de comentário. Para obter mais informações sobre esse caractere de comentário, consulte [barra dupla &#40;comentário&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md).  
  
-   **-(hífens duplos).** Use esses caracteres de comentário para gravar um comentário na mesma linha como código que deve ser executado, ou para gravar um comentário em uma linha por si próprio. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia tudo que estiver a partir das barras duplas até o final da linha como parte do comentário. Para criar um comentário de várias linhas, use os hífens duplos no início de cada linha de comentário. Para obter mais informações sobre esse caractere de comentário, consulte [– &#40;comentário&#41; &#40;DMX&#41; resumo](../dmx/comment-dmx-summary.md).  
  
-   **/\* ... \*/ (barra-asterisco pares de caracteres).** Use esses caracteres de comentário para gravar um comentário na mesma linha como o código que deve ser executado, para gravar um comentário em uma linha por si próprio ou até mesmo para gravar comentários dentro do código executável. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia tudo, desde o par de comentário de abertura (/ *) para o par de comentário de fechamento (\*/) como parte do comentário. Para criar um comentário de várias linhas, comece o comentário com o par de caracteres de comentário de abertura (/\*) e encerre o comentário com o par de caracteres de comentário de fechamento (\*/). Nenhum outro caractere de comentário deve ser incluído em qualquer linha do comentário. Para obter mais informações sobre esse caractere de comentário, consulte [estrela barra "/" &#40;comentário&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
