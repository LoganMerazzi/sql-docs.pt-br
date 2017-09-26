---
title: "Usando serviços de componentes da Microsoft | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: addf942a3813c1be918720756954eab14f6bc274
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-microsoft-component-services"></a>Usando serviços de componentes da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode habilitar um banco de dados Oracle trabalhar com serviços de componentes transacionais (ou MTS, se você estiver usando o Windows NT) no Microsoft Windows NT/Windows 2000 e Microsoft Windows 95/98. Para habilitar um banco de dados Oracle trabalhar com serviços de componentes que dão suporte a transações, os administradores do sistema devem criar uma exibição nomeada V$ XATRANS$. Para criar esse script, você deve executar um script fornecido pela Oracle. Para obter mais informações, consulte a Ajuda de serviços de componente ou a documentação do Oracle.