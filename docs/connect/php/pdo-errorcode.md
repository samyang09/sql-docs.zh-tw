---
title: PDO::errorCode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 143a7bef0a0be2d125068a7f003b0b941ff39617
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode 會擷取資料庫控制代碼上最新作業的 SQLSTATE。  
  
## <a name="syntax"></a>語法  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>傳回值  
PDO::errorCode 會以字串形式傳回五字元的 SQLSTATE；如果沒有資料庫控制代碼的作業，則傳回 NULL。  
  
## <a name="remarks"></a>備註  
PDO_SQLSRV 驅動程式中的 pdo:: errorcode 會針對某些成功的作業傳回警告。 例如，在成功連接之後，pdo:: errorcode 傳回"01000"，指出 SQL_SUCCESS_WITH_INFO。  
  
PDO::errorCode 只會針對直接在資料庫連接上執行作業擷取錯誤碼。 如果您建立 PDOStatement 執行個體透過 pdo:: prepare 或 pdo:: query 和錯誤所產生的陳述式物件，pdo:: errorcode 將不會擷取該錯誤。 您必須呼叫 PDOStatement::errorCode，才能傳回在特定陳述式物件上執行之作業的錯誤碼。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
在此範例中，資料行名稱的拼字錯誤 (`Cityx`而不是`City`)，導致發生錯誤，而後會予以報告。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
