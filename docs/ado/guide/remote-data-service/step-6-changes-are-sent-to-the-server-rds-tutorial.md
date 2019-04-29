---
title: 'Etapa 6: As alterações são enviadas ao servidor (Tutorial RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bfeb9ad607fc35c055e025fcc67435323d3143e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955713"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>Etapa 6: As alterações são enviadas ao servidor (Tutorial RDS)
Se o **Recordset** objeto é editado, todas as alterações (ou seja, linhas que são adicionadas, alteradas ou excluídas) podem ser enviadas de volta para o servidor.  
  
> [!NOTE]
>  O comportamento padrão do RDS pode ser chamado implicitamente com objetos do ADO e o Microsoft OLE DB comunicação remota do provedor. As consultas podem retornar **conjunto de registros**s e editados **Recordset**s pode atualizar a fonte de dados. Este tutorial não invoca o RDS com objetos do ADO, mas isso é como ela ficaria se tivesse:  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **A parte** pressupor para esse caso de você ter usado somente o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) e que um **conjunto de registros** objeto agora está associado a **RDS. DataControl**. O [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) método atualiza a fonte de dados com todas as alterações para o **conjunto de registros** objeto se o [servidor](../../../ado/reference/rds-api/server-property-rds.md) e [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propriedades ainda são definidas.  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **A parte B** como alternativa, você pode atualizar o servidor com o [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto, especificando uma conexão e uma **conjunto de registros** objeto.  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **Este é o fim do tutorial.**  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Comunicação remota do Microsoft OLE DB Provider (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
