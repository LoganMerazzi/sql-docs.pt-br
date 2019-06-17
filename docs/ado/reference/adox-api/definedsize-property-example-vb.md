---
title: Exemplo da propriedade DefinedSize (VB) | Microsoft Docs
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
- DefinedSize property [ADOX], Visual Basic example
ms.assetid: 4dda2239-7ab5-4729-9c63-eb530803f7d9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 67e0d2f3b98a54cd914739e62536080c3f9cc88f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697139"
---
# <a name="definedsize-property-example-vb"></a>Exemplo da propriedade DefinedSize (VB)
Este exemplo demonstra a [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) propriedade de uma [coluna](../../../ado/reference/adox-api/column-object-adox.md). O código irá redefinir o tamanho da coluna FirstName do **funcionários** tabela da *Northwind* banco de dados. Em seguida, a alteração nos valores de FirstName [campo](../../../ado/reference/ado-api/field-object.md) de uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) com base no **funcionários** tabela é exibida. Observe que por padrão, o campo FirstName fica preenchido com espaços após você redefinir o **DefinedSize** propriedade.  
  
```  
' BeginDefinedSizeVB  
Public Sub Main()  
    On Error GoTo DefinedSizeXError  
  
    Dim rstEmployees As ADODB.Recordset  
    Dim catNorthwind As New ADOX.Catalog  
    Dim colFirstName As ADOX.Column  
    Dim colNewFirstName As New ADOX.Column  
    Dim aryFirstName() As String  
    Dim i As Integer  
    Dim strCnn As String  
  
    strCnn = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
             "Data Source='Northwind.mdb';"  
  
    ' Open a Recordset for the Employees table.  
    Set rstEmployees = New ADODB.Recordset  
    rstEmployees.Open "Employees", strCnn, adOpenKeyset, , adCmdTable  
    ReDim aryFirstName(rstEmployees.RecordCount)  
  
    ' Open a Catalog for the Northwind database,  
    ' using same connection as rstEmployees  
    Set catNorthwind.ActiveConnection = rstEmployees.ActiveConnection  
  
    ' Loop through the recordset displaying the contents  
    ' of the FirstName field, the field's defined size,  
    ' and its actual size.  
    ' Also store FirstName values in aryFirstName array.  
    rstEmployees.MoveFirst  
    Debug.Print " "  
    Debug.Print "Original Defined Size and Actual Size"  
    i = 0  
    Do Until rstEmployees.EOF  
        Debug.Print "Employee name: " & rstEmployees!FirstName & _  
            " " & rstEmployees!LastName  
        Debug.Print "    FirstName Defined size: " _  
            & rstEmployees!FirstName.DefinedSize  
        Debug.Print "    FirstName Actual size: " & _  
            rstEmployees!FirstName.ActualSize  
            If Not rstEmployees!FirstName = Null Then  
                aryFirstName(i) = rstEmployees!FirstName  
            End If  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    ' Redefine the DefinedSize of FirstName in the catalog  
    Set colFirstName = catNorthwind.Tables("Employees").Columns("FirstName")  
    colNewFirstName.Name = colFirstName.Name  
    colNewFirstName.Type = colFirstName.Type  
    colNewFirstName.DefinedSize = colFirstName.DefinedSize + 1  
  
    ' Append new FirstName column to catalog  
    catNorthwind.Tables("Employees").Columns.Delete colFirstName.Name  
    catNorthwind.Tables("Employees").Columns.Append colNewFirstName  
  
    ' Open Employee table in Recordset for updating  
    rstEmployees.Open "Employees", catNorthwind.ActiveConnection, _  
        adOpenKeyset, adLockOptimistic, adCmdTable  
  
    ' Loop through the recordset displaying the contents  
    ' of the FirstName field, the field's defined size,  
    ' and its actual size.  
    ' Also restore FirstName values from aryFirstName.  
    rstEmployees.MoveFirst  
    Debug.Print " "  
    Debug.Print "New Defined Size and Actual Size"  
    i = 0  
    Do Until rstEmployees.EOF  
        rstEmployees!FirstName = aryFirstName(i)  
        Debug.Print "Employee name: " & rstEmployees!FirstName & _  
            " " & rstEmployees!LastName  
        Debug.Print "    FirstName Defined size: " _  
            & rstEmployees!FirstName.DefinedSize  
        Debug.Print "    FirstName Actual size: " & _  
            rstEmployees!FirstName.ActualSize  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    ' Restore original FirstName column to catalog  
    catNorthwind.Tables("Employees").Columns.Delete colNewFirstName.Name  
    catNorthwind.Tables("Employees").Columns.Append colFirstName  
  
    ' Restore original FirstName values to Employees table  
    rstEmployees.Open "Employees", catNorthwind.ActiveConnection, _  
        adOpenKeyset, adLockOptimistic, adCmdTable  
  
    rstEmployees.MoveFirst  
    i = 0  
    Do Until rstEmployees.EOF  
        rstEmployees!FirstName = aryFirstName(i)  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    'Clean up  
    Set catNorthwind = Nothing  
    Set colNewFirstName = Nothing  
    Set colFirstName = Nothing  
    Set rstEmployees = Nothing  
    Exit Sub  
  
DefinedSizeXError:  
    Set catNorthwind = Nothing  
    Set colNewFirstName = Nothing  
    Set colFirstName = Nothing  
  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndDefinedSizeVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Propriedade DefinedSize (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md)
