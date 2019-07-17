---
title: Colunas do conjunto de resultados de associação | Microsoft Docs
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
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: becda51a0fac924fce31e6cb15331321990d8a42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134998"
---
# <a name="binding-result-set-columns"></a>Associar colunas de conjunto de resultados
Aplicativos podem associar como muitas ou poucas colunas do conjunto de resultados conforme desejarem, incluindo nenhuma coluna de associação em todos os. Quando uma linha de dados for encontrada, o driver retorna os dados para as colunas associadas ao aplicativo. Se o aplicativo associa todas as colunas no conjunto de resultados depende do aplicativo. Por exemplo, aplicativos que geram relatórios geralmente têm um formato fixo; tais aplicativos criar um conjunto de resultados que contém todas as colunas usadas no relatório e, em seguida, associar e recuperam os dados de todas essas colunas. Aplicativos que exibem as telas cheio de dados, às vezes, permitir que o usuário decidir quais colunas serão exibidas; tais aplicativos criam um conjunto de resultados contendo todas as colunas que o usuário pode desejar, mas associar e recuperar os dados somente para as colunas escolhidos pelo usuário.  
  
 Dados podem ser recuperados de colunas não associadas, chamando **SQLGetData**. Isso normalmente é chamado para recuperar dados longos, que geralmente excede o comprimento de um único buffer e devem ser recuperados em partes.  
  
 Colunas podem ser associadas a qualquer momento, mesmo depois de linhas foram buscadas. No entanto, as novas associações não têm efeito até a próxima vez em que uma linha é buscada; eles não são aplicados aos dados de linhas buscadas já.  
  
 Uma variável permanece associada a uma coluna até que uma variável diferente é associada à coluna, até que a coluna é desassociada chamando **SQLBindCol** com um ponteiro nulo como o endereço da variável, até que todas as colunas são desassociadas chamando **SQLFreeStmt** com a opção SQL_UNBIND, ou até que a instrução seja liberada. Por esse motivo, o aplicativo deve ser-se de que todas as variáveis associadas permaneçam válidas, desde que eles estão ligados. Para obter mais informações, consulte [alocando e liberando Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Como as associações de coluna são apenas as informações associadas com a estrutura da instrução, elas podem ser definidas em qualquer ordem. Eles também são independentes do conjunto de resultados. Por exemplo, suponha que um aplicativo associa as colunas do conjunto de resultados gerado pela instrução SQL a seguir:  
  
```  
SELECT * FROM Orders  
```  
  
 Se o aplicativo, em seguida, executa a instrução SQL  
  
```  
SELECT * FROM Lines  
```  
  
 no mesmo identificador de instrução, as associações de coluna para o primeiro conjunto de resultados ainda estão em efeito porque eles são as associações armazenadas na estrutura da instrução. Na maioria dos casos, isso é uma prática inadequada de programação e deve ser evitado. Em vez disso, o aplicativo deve chamar **SQLFreeStmt** com a opção SQL_UNBIND desvincular todas as colunas antigas e, em seguida, associar novas.
