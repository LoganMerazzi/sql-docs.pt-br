---
title: Componentes ODBC afetados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08997f610b00f22d436a5c91d34beb2a8fc2cc1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944850"
---
# <a name="affected-odbc-components"></a>Componentes ODBC afetados
Compatibilidade com versões anteriores descreve como os aplicativos, o Gerenciador de Driver e os drivers são afetados pela introdução de uma nova versão do Gerenciador de Driver. Isso afeta aplicativos e o driver quando um ou ambos, eles permanecem na versão antiga. Há, portanto, três tipos de compatibilidade com versões anteriores a serem consideradas, conforme mostrado na tabela a seguir.  
  
|type|Versão do DM|Versão do aplicativo|Versão do driver|  
|----------|-------------------|----------------------------|-----------------------|  
|Compatibilidade com versões anteriores do Gerenciador de Driver|*3.x*|*2.x*|*2.x*|  
|Compatibilidade com versões anteriores do Driver [1]|*3.x*|*2.x*|*3.x*|  
|Compatibilidade com versões anteriores do aplicativo|*3.x*|*3.x*|*2.x*|  
  
 [1] a compatibilidade com versões anteriores dos drivers principalmente é discutida no Apêndice g: Diretrizes de driver para compatibilidade com versões anteriores.  
  
> [!NOTE]
>  Um aplicativo compatível com os padrões - por exemplo, um aplicativo que tenha sido gravado de acordo com os padrões Open Group ou a CLI de ISO - é garantido para trabalhar com ODBC *3.x* driver por meio de ODBC *3.x*Gerenciador de driver. Supõe-se que a funcionalidade que o aplicativo está usando está disponível no driver. Também supõe que o aplicativo compatível com os padrões foi compilado com o ODBC *3.x* arquivos de cabeçalho.
