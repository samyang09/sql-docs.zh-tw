---
title: "setHoldability 方法 (SQLServerConnection) |Microsoft 文件"
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
apiname: SQLServerConnection.setHoldability
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3494ece8b01fd59e0393662dd70caad7613758e9
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="setholdability-method-sqlserverconnection"></a>setHoldability 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  變更的保留性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)建立使用此物件[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)給定的保留性的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>參數  
 *nNewHold*  
  
 **Int**包含下列保留性等級的其中一個值：  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setHoldability 方法是由 java.sql.Connection 介面中的 setHoldability 方法指定。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
