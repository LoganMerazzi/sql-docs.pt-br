---
title: Compatibilidade com versões anteriores no SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 2f986436-aaf2-4eaf-9809-df849d97d4fb
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7a002b4f5d4b678171fc5dd396152d155779f78b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126774"
---
# <a name="backward-compatibility-in-smo"></a>Compatibilidade com versões anteriores no SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Os aplicativos SMO que foram escritos em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser recompilados com o SMO no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="migrating-smo-applications"></a>Migrando aplicativos SMO  
 As referências a dlls do SMO em versões mais antigas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser removidas, e as referências às novas dlls do SMO fornecidas com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] devem ser incluídas.  
  
 No mínimo, você faria as seguintes referências:  
  
-   Microsoft.SqlServer.ConnectionInfo  
  
-   Microsoft.SqlServer.Smo  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc  
  
 Esses arquivos são necessários para classes de conexão, classes de utilitário do SMO e classes de base.  
  
> [!NOTE]  
>  O arquivo SmoEnum.dll foi removido; portanto, as referências a ele devem ser removidas do projeto [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SMO.  
  
 Os namespaces também mudaram e você poderá usar o seguinte:  
  
##### <a name="for-visual-c"></a>Para o Visual C#  
  
```  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
```  
  
##### <a name="for-visual-basic"></a>Para o Visual Basic  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
```  
  
 Se o seu código usa a funcionalidade Urn, como **Server.GetSqlSmoObject(Urn)** , você deve estabelecer um vínculo com o namespace Microsoft.SqlServer.Management.Sdk.Sfc.  
  
 Se o seu código usar o objeto Transfer diretamente, você deverá estabelecer um vínculo com o namespace Microsoft.SqlServer.Management.SmoExtended.  
  
 Ao migrar o código, talvez seja necessário modificá-lo. Isso ocorre porque vários recursos do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] foram preteridos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações sobre recursos substituídos, consulte [recursos do mecanismo de banco de dados preteridos no SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md) em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Manuais Online.  
  
  
