---
title: Função do Gerenciador de Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7184c8ac9e0ad1813999a276f1579351f98544ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020404"
---
# <a name="role-of-the-driver-manager"></a>Função do Gerenciador do Driver
O Gerenciador de Driver determina a ordem final no qual retornar os registros de status que ele gera. Em particular, ele determina qual registro tem a classificação mais alta e deve ser retornado pela primeira vez. O driver é responsável por ordenar registros de status que ele gera. Se os registros de status são lançados pelo Gerenciador de Driver e o driver, o Gerenciador de Driver é responsável pela ordenação-los. Para obter mais informações, consulte [sequência de registros de Status](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 O Gerenciador de Driver não tanta verificação de erro possível. Isso salva cada driver de verificação para os mesmos erros. Por exemplo, se um argumento de função aceita um número distinto de valores, como *operação* na **SQLSetPos**, o Gerenciador de Driver verifica se o valor especificado é válido.  
  
 As seções a seguir descrevem os tipos de condições verificadas pelo Gerenciador de Driver. Elas não pretendem ser completa; Para obter uma lista completa das SQLSTATEs retorna o Gerenciador de Driver, consulte a seção de "Diagnóstico" de cada função; a descrição de cada verificação feita pelo Gerenciador de Driver começa com as letras "(DM)". Consulte também as tabelas de transição de estado no [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); erros mostrados entre parênteses são detectados pelo Gerenciador de Driver.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Verificações de valor de argumento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Verificações de transição de estado](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Verificações de erro gerais](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Verificações de aviso e de erro do Gerenciador de Driver](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
