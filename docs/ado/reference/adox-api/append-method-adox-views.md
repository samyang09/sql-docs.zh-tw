---
title: "Append 方法 (ADOX Views) |Microsoft 文件"
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
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5db1507f6574567cc6acd54e9ede053e36f1552
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-adox-views"></a>Append 方法 （ADOX 檢視）
建立新[檢視](../../../ado/reference/adox-api/view-object-adox.md)物件，並將它附加[檢視](../../../ado/reference/adox-api/views-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 A**字串**值，指定要建立之檢視的名稱。  
  
 *Command*  
 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，表示要建立的檢視。  
  
## <a name="remarks"></a>備註  
 具有名稱和屬性中指定的資料來源中建立新的檢視**命令**物件。  
  
 如果使用者指定的命令文字表示程序，而不是檢視，則行為是取決於提供者。 **附加**如果提供者不支援持續性命令將會失敗。  
  
> [!NOTE]
>  使用 Microsoft Jet OLE DB 提供者時**檢視**集合**附加**方法將允許您指定**程序**而不是**檢視**中*命令*參數。 **程序**會加入至資料來源，就會加入至**檢視**集合。 之後**附加**，如果**程序**和**檢視**重新整理集合時，**程序**將不再處於**檢視**集合會出現在**程序**集合。  
  
## <a name="applies-to"></a>適用於  
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [檢視附加方法範例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append 方法 （ADOX 資料行）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 群組）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 索引鍵）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 程序）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 資料表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)
