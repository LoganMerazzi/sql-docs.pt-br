---
title: Acrescente e exemplo dos métodos CreateParameter (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- CreateParameter method [ADO], Visual Basic example
- Append method [ADO], Visual Basic example
ms.assetid: 46908cbd-434f-43e7-a794-ed0be0e0c0a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60ea4653fac6bd2fada500d562420b1ff705d4d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920713"
---
# <a name="append-and-createparameter-methods-example-vb"></a>Exemplo dos métodos Append e CreateParameter (VB)
Este exemplo usa o [Append](../../../ado/reference/ado-api/append-method-ado.md) e [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) métodos para executar um procedimento armazenado com um parâmetro de entrada.  
  
```  
'BeginAppendVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset, command and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim cmdByRoyalty As ADODB.Command  
    Dim prmByRoyalty As ADODB.Parameter  
    Dim rstByRoyalty As ADODB.Recordset  
    Dim rstAuthors As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
    Dim strSQLByRoyalty As String  
     'record variables  
    Dim intRoyalty As Integer  
    Dim strAuthorID As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open command object with one parameter  
    Set cmdByRoyalty = New ADODB.Command  
    cmdByRoyalty.CommandText = "byroyalty"  
    cmdByRoyalty.CommandType = adCmdStoredProc  
  
    ' Get parameter value and append parameter  
    intRoyalty = Trim(InputBox("Enter royalty:"))  
    Set prmByRoyalty = cmdByRoyalty.CreateParameter("percentage", adInteger, adParamInput)  
    cmdByRoyalty.Parameters.Append prmByRoyalty  
    prmByRoyalty.Value = intRoyalty  
  
    ' Create recordset by executing the command  
    Set cmdByRoyalty.ActiveConnection = Cnxn  
    Set rstByRoyalty = cmdByRoyalty.Execute  
  
    ' Open the Authors Table to get author names for display  
    ' and set cursor client-side  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adUseClient, adLockOptimistic, adCmdTable  
  
    ' Print recordset adding author names from Authors table  
    Debug.Print "Authors with " & intRoyalty & " percent royalty"  
  
    Do Until rstByRoyalty.EOF  
        strAuthorID = rstByRoyalty!au_id  
        Debug.Print "   " & rstByRoyalty!au_id & ", ";  
        rstAuthors.Filter = "au_id = '" & strAuthorID & "'"  
        Debug.Print rstAuthors!au_fname & " " & rstAuthors!au_lname  
        rstByRoyalty.MoveNext  
    Loop  
  
    ' clean up  
    rstByRoyalty.Close  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstByRoyalty = Nothing  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstByRoyalty Is Nothing Then  
        If rstByRoyalty.State = adStateOpen Then rstByRoyalty.Close  
    End If  
    Set rstByRoyalty = Nothing  
  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndAppendVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)
