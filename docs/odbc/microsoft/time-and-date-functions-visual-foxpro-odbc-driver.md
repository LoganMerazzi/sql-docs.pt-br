---
title: Funções de hora e data (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 537af13edf943e27a634d3a8ba4f0f85c645251f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912400"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Funções de data e hora (Driver ODBC do Visual FoxPro)
A tabela a seguir lista as funções de data e hora ODBC compatíveis com o Driver ODBC para Visual FoxPro; Quando a gramática do Visual FoxPro para a mesma função difere da sintaxe ODBC, o Visual FoxPro equivalente é listado.  
  
|Gramática ODBC|Gramática do Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE *)*|DATA *)*|  
|FUNÇÃO CURTIME *)*|TEMPO *)*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH(*date_exp)*|DIA *)*|  
|HOUR *(time_exp)*||  
|MINUTE *(time_exp)*||  
|MONTH *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|AGORA *)*|DATETIME *( )*|  
|SECOND *(time_exp)*|SEC *(time_exp)*|  
|SEMANA *(date_exp)*||  
|ANO *(date_exp)*||  
  
 Não há suporte para as seguintes funções de data e hora:  
  
 DAYOFYEAR *(date_exp)*  
  
 TRIMESTRE *(date_exp)*  
  
 TIMESTAMPADD *(intervalo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(intervalo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Sequências de escape do ODBC  
 O driver também oferece suporte a sequência de escape ODBC para dados de data e o carimbo de hora. A sintaxe da cláusula de escape é da seguinte maneira:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 Nesta sintaxe **1!d** indica que *valor* é uma data no *aaaa-mm-dd* formato e **ts** indica que *valor*  é um carimbo de hora a *aaaa-mm-dd hh*[.*f...* ] formato. A sintaxe abreviada para dados de data e o carimbo de hora é da seguinte maneira:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Por exemplo, cada uma das instruções a seguir atualiza a tabela ALLTYPES usando a sintaxe abreviada de data e o carimbo de hora em um comando de atualização do SQL com suporte:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre sequências de escape, consulte [sequências de Escape no ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) na *referência do programador de ODBC*.
