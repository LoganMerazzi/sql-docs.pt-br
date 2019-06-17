---
title: 'Etapa 3: Compilar e executar uma instrução SQL | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3427057e70ee27fe1108fde71c833f0c511836b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148963"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Etapa 3: Criar e executar uma instrução SQL
A terceira etapa é compilar e executar uma instrução SQL, conforme mostrado na ilustração a seguir. Os métodos usados para executar esta etapa provavelmente podem variar muito. O aplicativo pode solicitar que o usuário digite uma instrução SQL, crie uma instrução SQL com base na entrada do usuário, ou usar uma instrução de SQL embutido em código. Para obter mais informações, consulte [construindo instruções de SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Mostra a criação e execução de uma instrução SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Se a instrução SQL contiver parâmetros, o aplicativo associa-las a variáveis de aplicativo, chamando **SQLBindParameter** para cada parâmetro. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Depois que a instrução SQL é criada e todos os parâmetros são associados, a instrução é executada com **SQLExecDirect**. Se a instrução for executada várias vezes, pode ser preparado com **SQLPrepare** e são executados com **SQLExecute**. Para obter mais informações, consulte [executando uma instrução](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 O aplicativo pode também abrir mão de execução de uma instrução SQL completa e em vez disso, chame uma função para retornar um conjunto de resultados que contém informações de catálogo, como as tabelas ou colunas disponíveis. Para obter mais informações, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Próxima de ação do aplicativo depende do tipo de instrução SQL executada.  
  
|Tipo de instrução SQL|Vá para|  
|---------------------------|----------------|  
|**Selecione** ou função de catálogo|[Etapa 4a: Buscar os resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**ATUALIZAÇÃO**, **exclua**, ou **inserir**|[Etapa 4b: Buscar a contagem de linhas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas as outras instruções SQL|Etapa 3: Compilar e executar uma instrução SQL (neste tópico) ou [etapa 5: Confirmar a transação](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
