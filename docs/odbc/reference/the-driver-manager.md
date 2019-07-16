---
title: O Gerenciador de Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 659678451c368df0b6a213e54cf7edaedfc29bd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039332"
---
# <a name="the-driver-manager"></a>O Gerenciador de Driver
O *Gerenciador de Driver* é uma biblioteca que gerencia a comunicação entre aplicativos e drivers. Por exemplo, nas plataformas do Microsoft® Windows®, o Gerenciador de Driver é uma biblioteca de vínculo dinâmico (DLL) que é escrita pela Microsoft e pode ser redistribuída por usuários de que o SDK do MDAC 2.8 SP1 do redistribuível.  
  
 O Gerenciador de Driver existe principalmente como uma conveniência para programadores e resolve diversos problemas comuns a todos os aplicativos. Isso inclui determinar qual driver carregar com base em um nome de fonte de dados, carregar e descarregar drivers e chamando funções em drivers.  
  
 Para ver por que o último é um problema, considere o que aconteceria se o aplicativo de funções chamadas no driver diretamente. A menos que o aplicativo foi vinculado diretamente a um driver específico, ele teria que criar uma tabela de ponteiros para as funções no driver e chamar essas funções pelo ponteiro. Usando o mesmo código para mais de um driver por vez, você adicionaria ainda outro nível de complexidade. O aplicativo primeiro precisa definir um ponteiro de função para apontar para a função correta no driver correto e, em seguida, chame a função através desse ponteiro.  
  
 O Gerenciador de Driver resolve esse problema, fornecendo um único lugar para chamar cada função. O aplicativo está vinculado às funções de ODBC Driver Manager e chamadas no Gerenciador de Driver, não o driver. O aplicativo identifica a fonte de dados e driver de destino com um *identificador de conexão*. Quando ele carregar um driver, o Gerenciador de Driver cria uma tabela de ponteiros para as funções no driver. Ele usa o identificador de conexão passado pelo aplicativo para localizar o endereço da função no driver de destino e chama essa função por endereço.  
  
 Geralmente, o Gerenciador de Driver passa apenas chamadas de função do aplicativo para o driver correto. No entanto, ele também implementa algumas funções (**SQLDataSources**, **SQLDrivers**, e **SQLGetFunctions**) e executa a verificação de erros básicos. Por exemplo, o Gerenciador de Driver verifica que os identificadores não são ponteiros nulos, que são chamadas de funções na ordem correta e que determinados argumentos de função são válidos. Para obter uma descrição completa dos erros verificados pelo Gerenciador de Driver, consulte a seção de referência para cada função e [apêndice b: Tabelas de transição de estado ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 A função de principal do Gerenciador de Driver final é carregar e descarregar drivers. O aplicativo carrega e descarrega apenas o Gerenciador de Driver. Quando desejar usar um driver específico, ele chama uma função de conexão (**SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**) no Gerenciador de Driver e especifica o nome de uma determinada fonte de dados ou driver, como "Contabilidade" ou "SQL Server". O Gerenciador de Driver usando esse nome, procura informações de fonte de dados para o nome de arquivo do driver, como Sqlsrvr.dll. Em seguida, carrega o driver (supondo que não tenha sido carregado), armazena o endereço de cada função no driver e chama a função de conexão no driver, que, em seguida, inicializa a próprio e conecta-se à fonte de dados.  
  
 Quando o aplicativo é feito usando o driver, ele chama **SQLDisconnect** no Gerenciador de Driver. O Gerenciador de Driver chamará essa função no driver, que desconecta da fonte de dados. No entanto, o Gerenciador de Driver mantém o driver na memória, no caso do aplicativo se reconecta a ele. Ele descarrega o driver somente quando o aplicativo libera a conexão usada pelo driver ou usa a conexão para um driver diferente, e nenhuma outra conexão usa o driver. Para obter uma descrição completa da função do Gerenciador de Driver ao carregar e descarregar drivers, consulte [do Gerenciador de Driver de função no processo de Conexão](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
