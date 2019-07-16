---
title: Conectar-se diretamente a Drivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44b9de304069849e965fc335e130ae57d9ec8bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083160"
---
# <a name="connecting-directly-to-drivers"></a>Conectar-se diretamente a drivers
Conforme foi discutido [escolhendo uma fonte de dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md), anteriormente nesta seção, alguns aplicativos não quiser usar uma fonte de dados em todos os. Em vez disso, eles querem se conectar diretamente a um driver. **SQLDriverConnect** fornece uma maneira para o aplicativo para se conectar diretamente a um driver sem especificar uma fonte de dados. Conceitualmente, uma fonte de dados temporário é criada em tempo de execução.  
  
 Para se conectar diretamente a um driver, o aplicativo especifica o **DRIVER** palavra-chave na cadeia de conexão em vez da **DSN** palavra-chave. O valor de **DRIVER** palavra-chave é a descrição do driver como retornado por **SQLDrivers**. Por exemplo, suponha que um driver tem a descrição do Driver do Paradox e requer um nome de um diretório que contém os arquivos de dados. Para se conectar a esse driver, o aplicativo pode usar qualquer uma das seguintes cadeias de caracteres de conexão:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Com a primeira cadeia de caracteres, o driver não precisaria informações adicionais. Com a segunda cadeia de caracteres, o driver precisa solicitar o nome do diretório que contém os arquivos de dados.
