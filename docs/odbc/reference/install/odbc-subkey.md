---
title: Subchave ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8aad5171b98c54aa0c4adbde1a5678e4fd953640
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093960"
---
# <a name="odbc-subkey"></a>Subchave do ODBC
Os valores na subchave ODBC especificam as opções de rastreamento de ODBC. Essas opções são definidas por meio da guia de rastreamento da caixa de diálogo Administrador de fonte de dados ODBC exibida pelo **SQLManageDataSources**. A subchave do ODBC em si é opcional. O formato desses valores é conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Data|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-path*|  
  
 Os valores possuem o significado descrito na tabela a seguir.  
  
|Valor|Significado|  
|-----------|-------------|  
|Trace|Se o valor de rastreamento for definido, como 1 quando um aplicativo chama **SQLAllocHandle** com a opção SQL_HANDLE_ENV, o rastreamento está habilitado para o aplicativo de chamada.<br /><br /> Se a palavra-chave de rastreamento é definida como 0 quando um aplicativo chama **SQLAllocHandle** com a opção SQL_HANDLE_ENV, o rastreamento está desabilitado para o aplicativo de chamada. Este é o valor padrão.<br /><br /> Um aplicativo pode habilitar ou desabilitar o rastreamento com o atributo de conexão SQL_ATTR_TRACE. No entanto, fazer então não altera os dados para esse valor.|  
|TraceFile|Se o rastreamento está habilitado, o Gerenciador de Driver grava o arquivo de rastreamento especificado pelo valor TraceFile.<br /><br /> Se nenhum arquivo de rastreamento for especificado, o Gerenciador de Driver grava no arquivo de log na unidade atual. Este é o valor padrão.<br /><br /> O rastreamento deve ser usado apenas para um único aplicativo, ou cada aplicativo deve especificar um arquivo de rastreamento diferentes. Caso contrário, duas ou mais aplicativos tentará abrir o mesmo arquivo de rastreamento ao mesmo tempo, causando um erro.<br /><br /> Um aplicativo pode especificar um novo arquivo de rastreamento com o atributo de conexão SQL_ATTR_TRACEFILE. No entanto, fazer então não altera os dados para esse valor.|  
  
 Por exemplo, suponha que o rastreamento está habilitado e o arquivo de rastreamento é C:\Odbc.log. Os valores na subchave ODBC seria da seguinte maneira:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
