---
title: Preenchimento de cadeia (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 29b7f35f41ede90c0b5cc54e336fb1d3e331ef81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967741"
---
# <a name="string-padding-ssis"></a>Preenchimento de cadeia (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O avaliador de expressão não verifica se uma cadeia de caracteres contém espaços à esquerda e à direita, e não preenche as cadeias de caracteres para que fiquem com o mesmo comprimento antes de compará-las. Se as expressões exigirem preenchimento de cadeia de caracteres, você poderá usar o operador + para concatenar valores de coluna e cadeias de caracteres vazias. Para obter mais informações, consulte [+ &#40;Concatenar&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/concatenate-ssis-expression.md).  
  
 Por ouro lado, se você quiser remover espaços, o avaliador de expressão fornece as funções LTRIM, RTRIM e TRIM, que removem os espaços à esquerda e/ou à direita. Para obter mais informações, consulte [LTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/ltrim-ssis-expression.md), [RTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/rtrim-ssis-expression.md) e [TRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/trim-ssis-expression.md).  
  
> [!NOTE]  
>  A função LEN inclui espaços em branco à esquerda e à direita em sua conta.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [SSIS Expression Cheat Sheet](https://go.microsoft.com/fwlink/?LinkId=746575), em pragmaticworks.com  
  
  
