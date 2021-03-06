---
title: "檢視附加方法範例 (VB) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b5b4c082-ac29-4f49-a8b8-e21b554c9b0d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 807c6ddff7af0c21f73a71a4457f9aba37e01a97
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="views-append-method-example-vb"></a>檢視附加方法範例 (VB)
下列程式碼示範如何使用[命令](../../../ado/reference/ado-api/command-object-ado.md)物件和[檢視](../../../ado/reference/adox-api/views-collection-adox.md)集合[附加](../../../ado/reference/adox-api/append-method-adox-views.md)方法基礎資料來源中建立新的檢視。  
  
```  
' BeginCreateViewVB  
Sub Main()  
    On Error GoTo CreateViewError  
  
    Dim cmd As New ADODB.Command  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the command representing the view.  
    cmd.CommandText = "Select * From Customers"  
  
    ' Create the new View  
    cat.Views.Append "AllCustomers", cmd  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set cmd = Nothing  
    Exit Sub  
  
CreateViewError:  
  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateViewVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection 屬性 (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Append 方法 （ADOX 檢視）](../../../ado/reference/adox-api/append-method-adox-views.md)   
 [目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [檢視物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)   
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
