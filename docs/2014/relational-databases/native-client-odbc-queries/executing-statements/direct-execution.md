---
title: Execução direta | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e912ac2dd63fa63ce57647f0c4e95e6702a22ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207072"
---
# <a name="direct-execution"></a>Execução direta
  A execução direta é o modo mais básico de executar uma instrução. Um aplicativo compila uma cadeia de caracteres contendo um [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução e o envia para execução usando o **SQLExecDirect** função. Quando a instrução alcança o servidor, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a compila em um plano de execução e executa esse plano imediatamente.  
  
 A execução direta normalmente é usada por aplicativos que compilam e executam instruções no tempo de execução e é o método mais eficiente para instruções que serão executadas de uma só vez. O problema com muitos bancos de dados é que a instrução SQL deve ser analisada e compilada sempre que é executada, o que adiciona sobrecarga se a instrução for executada várias vezes.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aprimora significativamente o desempenho da execução direta de instruções executadas comumente em ambientes de vários usuários, e o uso de SQLExecDirect com marcadores de parâmetro para instruções SQL usadas normalmente pode abordar a eficiência da execução preparada.  
  
 Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa o driver ODBC Native Client [sp_executesql](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql) para transmitir a instrução SQL ou lote especificado na **SQLExecDirect**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem uma lógica para determinar rapidamente se uma instrução SQL ou um lote executados com **sp_executesql** coincide com a instrução ou lote que gerou um plano de execução que já existe na memória. Se houver correspondência, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] simplesmente reutilizará o plano existente, em vez de compilar um novo plano. Isso significa que, comumente executadas instruções SQL executadas com **SQLExecDirect** em um sistema com muitos usuários se beneficiarão muitos dos benefícios de reutilização do plano que são disponíveis somente para procedimentos armazenados em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Esse benefício de reutilizar planos de execução só funciona quando vários usuários estiverem executando a mesma instrução ou lote SQL. Siga estas convenções de codificação para aumentar a probabilidade de as instruções SQL executadas por clientes diferentes serem semelhantes a ponto de permitirem a reutilização de planos de execução:  
  
-   Não inclua constantes de dados nas instruções SQL; em vez disso, use marcadores de parâmetro associados para programar variáveis. Para obter mais informações, consulte [usando parâmetros de instrução](../using-statement-parameters.md).  
  
-   Use nomes de objeto totalmente qualificados. Os planos de execução não serão reutilizados se os nomes de objeto não forem totalmente qualificados.  
  
-   Faça com que as conexões de aplicativo usem, na medida do possível, um conjunto comum de opções de conexão e instrução. Os planos de execução gerados para uma conexão com um conjunto de opções (como ANSI_NULLS) não são reutilizados para uma conexão que tenha outro conjunto de opções. O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client têm as mesmas configurações padrão para essas opções.  
  
 Se todas as instruções executadas com **SQLExecDirect** são codificadas usando essas convenções, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode reutilizar planos de execução quando a oportunidade ocorrer.  
  
## <a name="see-also"></a>Consulte também  
 [Executar instruções &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
