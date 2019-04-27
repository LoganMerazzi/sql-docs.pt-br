---
title: Suporte (Driver ODBC do Visual FoxPro) do thread | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77187802bb57a832263ec2070564754e87f21345
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632919"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Suporte a thread (Driver ODBC do Visual FoxPro)
O Driver de ODBC do Visual FoxPro é thread-safe. Acesso aos identificadores de ambiente (*uando*), identificadores de conexão (*hdbc*) e identificadores de instrução (*hstmt*) é encapsulado em semáforos apropriados para impedir que outros processos acesse e possivelmente alterar estruturas de dados internas do driver.  
  
 Em um aplicativo multithread, você pode cancelar uma função que está executando de forma síncrona em uma *hstmt* chamando [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) em um thread separado.  
  
 O driver usa um thread separado para buscar dados quando você usa a busca progressiva. Para usar a busca progressiva para uma fonte de dados, selecione a **buscar dados no plano de fundo** caixa de seleção a [caixa de diálogo de instalação do ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ou usar a palavra-chave de atributo BackgroundFetch em sua conexão cadeia de caracteres. Evite usar a busca em segundo plano quando você chama o driver de aplicativos multithread. Para obter informações sobre palavras-chave atributo de cadeia de caracteres de conexão, consulte [usando cadeias de caracteres de Conexão](../../odbc/microsoft/using-connection-strings.md).  
  
 Para obter mais informações sobre threads e **SQLCancel**, consulte [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) no *referência do programador de ODBC*.
