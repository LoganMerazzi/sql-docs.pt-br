---
title: Práticas recomendadas para chamar procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b78fe54f7643421328f6d6a2ec61544db725488
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951159"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>Práticas recomendadas para chamar procedimentos armazenados compilados nativamente
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Estes são os procedimentos armazenados compilados nativamente:  
  
-   Geralmente usados em partes essenciais do desempenho de um aplicativo.  
  
-   Executados com frequência.  
  
-   Espera-se que sejam muito rápidos.  
  
 O benefício em termos de desempenho com o uso de um procedimento armazenado compilado nativamente aumenta com o crescente número de linhas e a quantidade de lógica que é processada pelo procedimento. Por exemplo, um procedimento armazenado compilado nativamente exibirá o melhor desempenho se ele usar um ou mais dos seguintes itens:  
  
-   Agregação.  
  
-   Junções de loops aninhados.  
  
-   Operações de seleção, inserção, atualização e exclusão com várias instruções.  
  
-   Expressões complexas.  
  
-   Lógica de procedimento, como instruções condicionais e loops.  
  
 Se você precisa processar apenas uma única linha, usar um procedimento armazenado compilado nativamente talvez não traga um benefício em termos de desempenho.  
  
 Para evitar que o servidor precise mapear nomes de parâmetro e converter tipos:  
  
-   Faça a correspondência dos tipos dos parâmetros passados para o procedimento com os tipos contidos na definição de procedimento.  
  
-   Use parâmetros ordinais (sem nome) ao chamar procedimentos armazenados compilados nativamente. Para uma execução mais eficiente, não use parâmetros nomeados.  
  
 Ineficiências em parâmetros com procedimentos armazenados compilados nativamente podem ser detectadas com o XEvent **natively_compiled_proc_slow_parameter_passing**:
 - Tipos incompatíveis: **reason=parameter_conversion**
 - Parâmetros nomeados: **reason=named_parameters**
 - Valores PADRÃO: **reason=default** 
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
