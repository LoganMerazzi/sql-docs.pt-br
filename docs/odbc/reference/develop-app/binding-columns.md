---
title: Colunas de associação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a634a553672b83931091056dd489f7559c4269b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106211"
---
# <a name="binding-columns"></a>Colunas de associação
Os dados buscados da fonte de dados são retornados para o aplicativo em variáveis que o aplicativo alocado para essa finalidade. Antes de fazer isso, o aplicativo deve associar, ou *associar*, defina essas variáveis para as colunas de resultado; conceitualmente, esse processo é o mesmo que associando variáveis de aplicativo para parâmetros de instrução. Quando o aplicativo é associado a uma variável a uma coluna do conjunto de resultados, ele descreve - endereço, tipo de dados e assim por diante, essa variável para o driver. O driver armazena essas informações na estrutura, ele mantém para essa instrução e usa as informações para retornar o valor da coluna quando a linha é buscada.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associando colunas de conjunto de resultados](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
