---
title: Não permitido de tipos e membros no DLL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
ms.openlocfilehash: 50f7f8aacfc61b55e969ea0d57f82d58e50e093b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028123"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipos e membros não permitidos em System.Data.dll
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programação de integração (CLR) de linguagem comum não permite o uso de um tipo ou membro que tem um **HostProtectionAttribute** que especifica um **System.Security.Permissions.HostProtectionResource** enumeração com um valor de **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **sincronização**, ou **Interface do usuário**. A tabela a seguir lista os membros e os tipos do assembly System.Data.dll cujos valores de HPA (atributo de proteção de host) não são permitidos.  
  
> [!NOTE]  
>  Esta lista foi gerada dos assembly com suporte. Para obter mais informações, consulte [suporte para bibliotecas do .NET Framework](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo ou membro|Valor(es) de HPA|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery ()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor ()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start ()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Sincronização|  
|System.Xml.XmlDataDocument|Synchronization|  
  
## <a name="see-also"></a>Consulte também  
 [Atributos de proteção de host e programação da integração CLR](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos desaprovados e membros no VisualBasic](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos desaprovados e membros em mscorlib. dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos desaprovados e membros em System. dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [Tipos e membros não permitidos no System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
