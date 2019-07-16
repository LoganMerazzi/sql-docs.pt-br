---
title: Função SQLSetScrollOptions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ad13ef3d443e2c99a44ad1cbefbf9f08fa2e742
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039673"
---
# <a name="sqlsetscrolloptions-function"></a>Função SQLSetScrollOptions
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: Preterido  
  
 **Resumo**  
 Em ODBC *3.x*, a função ODBC 2.0 **SQLSetScrollOptions** foi substituído por chamadas para **SQLGetInfo** e **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC *2.x* aplicativo está funcionando com um ODBC *3.x* driver, consulte [preterido funções de mapeamento de](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)apêndice g: Diretrizes de driver para compatibilidade com versões anteriores.  
> 
> [!NOTE]
>  Quando o Gerenciador de Driver mapeia **SQLSetScrollOptions** para um aplicativo trabalhar com ODBC *3.x* driver não oferece suporte a **SQLSetScrollOptions**, o Driver Manager define a opção de instrução SQL_ROWSET_SIZE, não o atributo SQL_ATTR_ROW_ARRAY_SIZE instrução para o *RowsetSize* argumento **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele pode ser usado somente quando ao buscar várias linhas por uma chamada para **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Comentários  
 Se o aplicativo será executado em um sistema operacional de 64 bits, consulte [informações de ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
