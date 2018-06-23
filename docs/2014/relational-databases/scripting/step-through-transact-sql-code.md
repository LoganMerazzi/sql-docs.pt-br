---
title: Percorrer código Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Transact-SQL debugger, debugging code
- Transact-SQL debugger, step over
- Transact-SQL debugger, step out
- Transact-SQL debugger, step into
ms.assetid: e09079b8-c4c9-42b4-821b-4ce81a98a086
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6cb9a3f5e0d275e4b7b646401f81b8128546a850
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008618"
---
# <a name="step-through-transact-sql-code"></a>Percorrer código Transact-SQL
  O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] permite que você controle quais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] são executadas em uma janela Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Você pode pausar o depurador em instruções individuais e exibir o estado dos elementos de código nesse ponto.  
  
## <a name="breakpoints"></a>Pontos de interrupção  
 Um ponto de interrupção sinaliza o depurador para pausar a execução em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] específica. Para mais informações sobre pontos de interrupção, consulte Usando pontos de interrupção de Transact-SQL.  
  
## <a name="controlling-statement-execution"></a>Controlando a execução de uma instrução  
 No depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] , você pode especificar as seguintes opções para executar a partir da instrução atual em código [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
-   Executar até o próximo ponto de interrupção.  
  
-   Avançar para a próxima instrução.  
  
     Se a próxima instrução chamar um procedimento armazenado, uma função ou um gatilho do [!INCLUDE[tsql](../../includes/tsql-md.md)] , o depurador exibirá uma nova janela do Editor de Consultas que contém o código do módulo. A janela está no modo de depuração e a execução pausa na primeira instrução do módulo. Você pode mover-se pelo código do módulo, por exemplo, definindo pontos de interrupção ou percorrendo o código.  
  
-   Passe pela próxima instrução.  
  
     A próxima instrução é executada. No entanto, se a próxima instrução chamar um procedimento armazenado, uma função ou um gatilho, o código do módulo será executado até o fim, e os resultados serão retornados ao código de chamada. Se você tiver certeza de que não há erros em um procedimento armazenado, poderá passar por ele. A execução pausa na instrução que segue a chamada do procedimento armazenado, da função ou do gatilho.  
  
-   Sair de um procedimento armazenado, uma função ou um gatilho.  
  
     A execução pausa na instrução que segue a chamada do procedimento armazenado, da função ou do gatilho.  
  
-   Execute do local atual ao local atual do ponteiro e ignore todos os pontos de interrupção.  
  
 A tabela a seguir lista os vários modos nos quais você pode controlar como as instruções são executadas  no depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
|Ação|Procedimento|  
|------------|---------------|  
|Executar todas as instruções da instrução atual para o próximo ponto de interrupção|Sobre o **depurar** menu, clique em **continuar**.<br /><br /> Sobre o **depurar** barra de ferramentas, clique no **continuar** botão.|  
|Avançar para a próxima instrução ou módulo|Sobre o **depurar** menu, clique em **intervir**.<br /><br /> Sobre o **depurar** barra de ferramentas, clique no **intervir** botão.<br /><br /> Pressione F11.|  
|Passar pela próxima instrução ou módulo|Sobre o **depurar** menu, clique em **passar por**.<br /><br /> Sobre o **depurar** barra de ferramentas, clique no **passar por** botão.<br /><br /> Pressione F10.|  
|Sair de um módulo|Sobre o **depurar** menu, clique em **sair**.<br /><br /> Sobre o **depurar** barra de ferramentas, clique no **sair** botão.<br /><br /> Pressione SHIFT+F11.|  
|Executar para o local do cursor atual|Clique com o botão direito do mouse na janela Editor de Consultas e então clique em **Executar até o Cursor**.<br /><br /> Pressione CTRL+F10.|  
  
## <a name="see-also"></a>Consulte também  
 [Informações do depurador Transact-SQL](transact-sql-debugger-information.md)  
  
  