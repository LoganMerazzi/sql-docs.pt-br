---
title: Modos SQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6965d67b6dae484b3fa72f215446682f9aa6760c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028363"
---
# <a name="sql-modes-mysqltosql"></a>Modos SQL (MySQLToSQL)
O SSMA para MySQL pode operar em diferentes modos SQL e pode aplicar esses modos de forma diferente para diferentes clientes.  
  
Modos de definem a sintaxe SQL MySQL deve dar suporte e o tipo de validação de dados verifica que ele deve executar. Isso torna mais fácil de usar o MySQL em ambientes diferentes e usam o MySQL com o SQL Server.  
  
## <a name="sql-modes-grid"></a>Grade de modos SQL:  
  
-   Grade de modos SQL no nível raiz contém as seguintes colunas: **Nome do modo SQL**, **carregados modos SQL**, e **modos SQL eficaz**.  
  
-   Grade de modos de SQL em bancos de dados categoria, banco de dados, tabela categoria, categoria de instruções, categoria de exibições, tabelas, exibições, funções, procedimentos, UDF e o nível de objeto do evento contém as seguintes colunas: **Nome do modo SQL**, **herdadas modos SQL**, e **modos SQL eficaz**.  
  
-   Grade de modos SQL no nível de procedimento armazenado, função armazenado e disparador contém as seguintes colunas: **Nome do modo SQL**, **modos SQL Original**, e **modos SQL eficaz**.  
  
> [!NOTE]  
> Modos de grupo serão mostrados em negrito, sob a coluna 'Nome do modo SQL'.  
  
## <a name="loaded-sql-modes"></a>Modos SQL carregado  
Esses são os modos de SQL, que são definidas no nível da sessão ou raiz. Os modos SQL após o carregamento no banco de dados de destino não pode ser editados ou alterados.  
  
## <a name="inherited-sql-modes"></a>Modos SQL herdadas  
Esses são os modos SQL, que são herdadas a partir do nó pai correspondente.  
  
Exceto para a categoria de funções, categoria de procedimentos, categoria de eventos e gatilhos, esses modos SQL estão presentes em todos os níveis (objeto de banco de dados, tabela categoria, categoria de instruções, modos de exibição categoria, tabela, exibição, funções, procedimentos, UDF e eventos).  
  
> [!NOTE]  
> Selecionando o **herdar do pai** caixa de seleção, modos herdado do SQL podem ser herdada do nó pai. Por padrão, essa caixa de seleção permanece marcada.  
  
## <a name="original-sql-modes"></a>Modos SQL originais  
Esses são os modos SQL presentes em apenas os níveis de função, o procedimento e o gatilho.  
  
> [!NOTE]  
> Selecionando o **uso original** verificar caixa, os modos de SQL que foram originalmente usados na função correspondente ou o procedimento ou gatilho pode ser usado. Por padrão, essa caixa de seleção permanece marcada.  
  
## <a name="effective-sql-modes"></a>Modos SQL eficaz  
Modos de efetivas SQL pode ser definidos em vários níveis da seguinte maneira:  
  
-   **No nível de sessão:**  
  
    1.  Todos os modos de SQL carregado pode ser chamados, "Modos de efetivas SQL".  
  
    2.  Nesse nível, os modos SQL efetivos podem ser diretamente e explicitamente modificados.  
  
    3.  O modo SQL eficaz que é definido explicitamente não é refletido como modo de SQL carregado e, por fim, é aplicado ao objeto.  
  
-   **No nível de função ou procedimento ou Gatilho:**  
  
    1.  Todos os modos SQL Original pode ser chamado, "Modos de efetivas SQL".  
  
    2.  Nesse nível, o modo SQL eficaz pode ser modificado explicitamente somente quando o **uso original** caixa de seleção está desmarcada.  
  
    3.  O modo SQL eficaz que é definido explicitamente não é refletido como modo Original do SQL e, por fim, é aplicado ao objeto.  
  
-   **Em nós diferentes de nível de função ou procedimento ou Gatilho:**  
  
    1.  Todos os modos de SQL herdado pode ser chamados, "Modos de efetivas SQL".  
  
    2.  Nesse nível, o modo SQL eficaz pode ser modificado explicitamente somente quando o **herdar do pai** caixa de seleção está desmarcada.  
  
    3.  O modo SQL eficaz que é definido explicitamente não é refletido como modo herdado de SQL e, por fim, é aplicado ao objeto.  
  
