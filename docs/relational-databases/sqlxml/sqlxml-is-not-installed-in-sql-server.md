---
title: O SQLXML não é instalado no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2adac1703facccda712db1e3f5826f784c0be141
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135319"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>O SQLXML não é instalado no SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Antes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o SQLXML 4.0 era lançado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazia parte da instalação padrão de todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], com exceção da [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], a última versão do SQLXML (SQLXML 4.0 SP1) não está mais incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar o SQLXML 4.0 SP1, baixe-o do [local de instalação do SQLXML 4.0 SP1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 Se um aplicativo for executado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exigir o SQLXML 4.0, você precisa baixar e instalar o SQLXML 4.0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamento do SQLXML 4.0 SP1 com novos tipos de dados que usam o SQLOLEDB e o SQL Server Native Client OLE DB Provider  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduziu os seguintes tipos de dados, que os desenvolvedores usando o SQLXML talvez queira usar:  
  
-   **Data**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 Ao usar o SQLXML 4.0 SP1 com o SQLOLEDB ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], esses tipos são exibidos como cadeias de caracteres para um desenvolvedor. SQLXML 4.0 SP1 habilitará esses quatro novos tipos de dados como tipos escalares internos quando usados com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 ou posterior. Até que o SQLXML 4.0 SP1 seja baixado, o mapeamento desses tipos com tipos que não são de cadeias de caracteres pode provocar truncamento de alguns dados. Por exemplo, o mapeamento **DateTime2** à **xsd: Date** fará com que dados sejam truncados para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **DateTime** precisão de 3,33 milissegundos.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos de programação do SQLXML 4.0](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
