---
title: "更新的重新同步處理屬性動態 (ADO) |Microsoft 文件"
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
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6084a0075508c8a9a3658b4a8c694957409376c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="update-resync-property-dynamic-ado"></a>更新的重新同步處理屬性動態 (ADO)
指定是否[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法後面的隱含[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法作業，而且如果是，該作業的範圍。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回一或多個[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)值。  
  
## <a name="remarks"></a>備註  
 ADCPROP_UPDATERESYNC_ENUM 的值可能會合併，除了 adResyncAll 已經代表其餘的值的組合。  
  
 常數**adResyncConflicts**儲存重新同步處理的值為基礎的值，但不是會覆寫暫止的變更。  
  
 **更新的重新同步處理**動態屬性附加至[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
