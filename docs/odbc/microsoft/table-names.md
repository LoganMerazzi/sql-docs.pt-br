---
title: Nomes de tabela | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dd8de055521f4a1831d20a9a34bedb9309d1de6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939784"
---
# <a name="table-names"></a>Nomes de tabela
Quando o dBASE, Microsoft Excel, Paradox, ou texto driver é usado, nomes de tabela que ocorrem na cláusula FROM de SELECT ou DELETE, depois da cláusula INTO em INSERT e UPDATE, CREATE TABLE e DROP TABLE podem conter um caminho válido, nome primário e arquivo de extensão de nome .  
  
 Uso de um nome de tabela em outro lugar em uma instrução SQL não suporta o uso de caminhos ou extensões, mas aceitará somente o nome primário (por exemplo, EMP de C:\ABC\EMP).  
  
 Nomes de correlação (alias) podem ser usados. Por exemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
