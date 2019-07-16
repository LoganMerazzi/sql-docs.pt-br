---
title: Identificadores de instrução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 730ead7bf90af3b6e6906fe184e0fa3312212137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107264"
---
# <a name="statement-handles"></a>Identificadores de instrução
Um *instrução* é mais fácil pensar de como uma instrução SQL, tais como **selecionar \* do funcionário**. No entanto, uma instrução é mais do que apenas uma instrução SQL – ele consiste em todas as informações associadas a essa instrução SQL, como conjuntos de resultados criados pela instrução e os parâmetros usados na execução da instrução. Uma instrução não ainda precisa ter uma instrução de SQL definido pelo aplicativo. Por exemplo, quando uma função de catálogo, como **SQLTables** é executado em uma instrução, ele executa uma instrução SQL predefinida que retorna uma lista de nomes de tabela.  
  
 Cada instrução é identificada por um identificador de instrução. Uma instrução é associada uma única conexão e pode haver várias instruções em que a conexão. Alguns drivers de limitam o número de instruções ativas que dar suporte a eles; opção o SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo** Especifica quantas instruções ativas que oferece suporte a um driver em uma única conexão. Uma instrução é definida para ser *active* se ela tiver resultados pendentes, onde os resultados são um conjunto de resultados ou a contagem de linhas afetadas por uma **inserir**, **atualização**, ou **Excluir** instrução ou dados que estão sendo enviados com várias chamadas para **SQLPutData**.  
  
 Dentro de um trecho de código que implementa o ODBC (o Gerenciador de Driver ou um driver), o identificador de instrução identifica uma estrutura que contém informações sobre a instrução, como:  
  
-   Estado da instrução  
  
-   O diagnóstico de nível de instrução atual  
  
-   Os endereços das variáveis de aplicativo associados aos parâmetros da instrução e colunas do conjunto de resultados  
  
-   As configurações atuais de cada atributo de instrução  
  
 Identificadores de instrução são usados na maioria das funções ODBC. Em especial, elas são usadas nas funções para associar parâmetros e colunas do conjunto de resultados (**SQLBindParameter** e **SQLBindCol**), preparar e executar instruções (**SQLPrepare** **SQLExecute**, e **SQLExecDirect**), recuperar metadados (**SQLColAttribute** e **SQLDescribeCol**), fetch os resultados (**SQLFetch**) e recuperar o diagnóstico (**SQLGetDiagField** e **SQLGetDiagRec**). Eles também são usados em funções de catálogo (**SQLColumns**, **SQLTables**e assim por diante) e um número de outras funções.  
  
 Identificadores de instrução são alocados com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.
