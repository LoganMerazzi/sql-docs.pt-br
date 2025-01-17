---
title: Usando o Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 232ea094ac81badfe7a6ec378371b55a0b08103b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62518736"
---
# <a name="using-database-mail"></a>Usando o Database Mail
  No SMO, o subsistema Database Mail é representado pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> que é referenciado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A>. Através do objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> do SMO, você pode configurar o subsistema Database Mail e gerenciar perfis e contas de email. O objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> do SMO pertence ao objeto `Server`. Isso significa que o escopo das contas de email está em nível de servidor.  
  
## <a name="examples"></a>Exemplos  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um Visual C&#35; projeto de SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
 Para programas que usam [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Database Mail, você deve incluir o `Imports` instrução para qualificar o namespace do Mail. Insira a instrução após outras instruções `Imports`, antes de qualquer declaração no aplicativo, como:  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Criando uma conta de email de banco de dados usando o Visual Basic  
 Este exemplo de código mostra como criar uma conta de email no SMO. O Database Mail é representado pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e referenciado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. O SMO pode ser usado para configurar programaticamente o Database Mail, mas não pode ser usado para enviar ou tratar emails recebidos.  
  
 VB.NET  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMail1](SMO How to#SMO_VBMail1)]  -->  
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>Criando uma conta de email de banco de dados usando o Visual C#  
 Este exemplo de código mostra como criar uma conta de email no SMO. O Database Mail é representado pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e referenciado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. O SMO pode ser usado para configurar programaticamente o Database Mail, mas não pode ser usado para enviar ou tratar emails recebidos.  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>Criando uma conta de email de banco de dados usando o PowerShell  
 Este exemplo de código mostra como criar uma conta de email no SMO. O Database Mail é representado pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e referenciado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. O SMO pode ser usado para configurar programaticamente o Database Mail, mas não pode ser usado para enviar ou tratar emails recebidos.  
  
 PowerShell  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  
