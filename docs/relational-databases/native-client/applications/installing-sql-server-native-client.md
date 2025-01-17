---
title: Instalando o SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
author: MightyPen
ms.author: genemi
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dee5cebb97ff491595ca5e875c3adfc08c82bf2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987583"
---
# <a name="installing-sql-server-native-client"></a>Instalando o SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 é instalado quando você instala o [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]. 
 
 Não há nenhum SQL Server 2016 Native Client. Para obter mais informações, consulte [SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client.md). 
 
Você também pode obter sqlncli.msi na página da Web do SQL Server 2012 Feature Pack. Para baixar a versão mais recente do SQL Server Native Client, vá para [Microsoft® SQL Server® 2012 Feature Pack](https://www.microsoft.com/download/confirmation.aspx?id=29065). Se uma versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client anterior ao SQL Server 2012 também é instalado no computador, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 será instalada lado a lado com a versão anterior.  
  
 Os arquivos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli11.dll, sqlnclir11.rll e s11ch_sqlncli.chm) são instalados no seguinte local:  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  Todas as configurações do Registro apropriadas para o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fazem parte do processo de instalação.  
  
 Os arquivos de biblioteca e cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h e sqlncli11.lib) são instalados no seguinte local:  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 Além da instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como parte da instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], também há um programa de instalação redistribuível chamado sqlncli.msi, que se encontra no disco de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no seguinte local: `%CD%\Setup\`.  
  
 Você pode distribuir o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client através do sqlncli.msi. Talvez seja necessário instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ao implantar um aplicativo. Uma maneira de instalar vários pacotes em um processo que, para o usuário, parece ser uma única instalação é usar a tecnologia de encadeador e bootstrapper. Para obter mais informações, confira [Criando um pacote de bootstrapper personalizado para o Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) e [Adicionando pré-requisitos personalizados](https://go.microsoft.com/fwlink/?LinkId=115668).  
  
 As versões para x64 e Itanium de sqlncli.msi também instalam a versão de 32 bits do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Se o aplicativo foi projetado para uma plataforma diferente daquela em que foi desenvolvido, você poderá baixar as versões do sqlncli.msi para x64, Itanium e x86 do Centro de Download da Microsoft.  
  
 Quando você invoca o sqlncli.msi, só os componentes cliente são instalados por padrão. Os componentes de cliente são arquivos que dão suporte à execução de um aplicativo que foi desenvolvido usando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Para instalar também os componentes SDK, especifique `ADDLOCAL=All` na linha de comando. Por exemplo:  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>Instalação silenciosa  
 Se você usar a opção /passive, /qn, /qb, or /qr com msiexec, também deverá especificar IACCEPTSQLNCLILICENSETERMS=YES, para indicar explicitamente que aceitou os termos da licença do usuário final. Essa opção deve ser especificada totalmente em letras maiúsculas.  
  
## <a name="uninstalling-sql-server-native-client"></a>Desinstalando o SQL Server Native Client  
 Como aplicativos, como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ferramentas dependem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, é importante não desinstalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client até que todos os aplicativos dependentes são desinstalados. Para usuários do provedor com um aviso de que seu aplicativo depende [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, use a opção de instalação APPGUID no MSI, da seguinte maneira:  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 O valor passado para APPGUID é o seu código de produto específico. É preciso criar um código de produto ao usar o Microsoft Installer para agrupar o programa de instalação do aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)   
 [Tópicos de instruções sobre a instalação](https://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  
