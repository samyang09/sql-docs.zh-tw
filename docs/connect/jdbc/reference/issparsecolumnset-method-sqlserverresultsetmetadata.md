---
title: "isSparseColumnSet 方法 (SQLServerResultSetMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ac363670-78ae-49f1-aeda-4fba3329a258
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0486fd19f95b6a9b4d987c4b4dc7f1810e82543d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="issparsecolumnset-method-sqlserverresultsetmetadata"></a>isSparseColumnSet 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出結果集中的資料行是否為疏鬆資料行集。  
  
## <a name="syntax"></a>語法  
  
```scr  
public boolean isSparseColumnSet(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *資料行*  
  
 資料行的索引 (以一為基底)。  
  
## <a name="return-value"></a>傳回值  
 **true**如果結果集中的資料行是疏鬆資料行集，否則**false**。  
  
## <a name="remarks"></a>備註  
 此方法不會從資料庫中擷取資訊。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
