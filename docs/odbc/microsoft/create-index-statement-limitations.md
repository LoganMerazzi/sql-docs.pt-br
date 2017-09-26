---
title: "Criar índice instrução limitações | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 874aba454df680626a126f19faa821f885e9d040
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="create-index-statement-limitations"></a>Criar índice limitações de instrução
Não há suporte para a instrução CREATE INDEX para os drivers de texto ou do Microsoft Excel.  
  
 Um índice pode ser definido em um máximo de 10 colunas. Se mais de 10 colunas são incluídas em uma instrução CREATE INDEX, o índice não será reconhecido e a tabela será tratada como se nenhum índice foi criado.  
  
 O driver dBASE não é possível criar um índice em uma coluna lógica.  
  
 Quando o driver dBASE é usado, o tempo de resposta em grandes arquivos pode ser melhorado pela criação de um índice de MDX (ou ndx) na coluna (campo) especificados nas cláusulas WHERE de uma instrução SELECT. Os índices existentes. MDX serão aplicados automaticamente para =, >, \<, > =, = < e entre operadores em uma cláusula WHERE e predicados LIKE, bem como em predicados de junção.  
  
 Quando o driver dBASE é usado, o índice criado por uma instrução CREATE UNIQUE INDEX é na verdade não exclusivo, e podem ser inseridos valores duplicados na coluna indexada. Apenas um registro de um conjunto de valores de chave idênticos pode ser adicionado ao índice.  
  
 Quando o driver do Paradox é usado, um índice exclusivo deve ser definido em um subconjunto de contíguo de colunas em uma tabela, incluindo a primeira coluna. Uma tabela não pode ser atualizada pelo driver Paradox se um índice exclusivo não está definido na tabela ou quando o driver do Paradox é usado sem a implementação do BDE.