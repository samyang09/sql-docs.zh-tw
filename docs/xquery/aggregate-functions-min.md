---
title: "min 函數 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 113ef17b789527104d0b79e4521de14a8703c029
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="aggregate-functions---min"></a>彙總函式的最小值
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  從不可部份完成值的序列傳回*$arg*，其值必須小於所有其他的項目。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 從項目序列傳回最小值。  
  
## <a name="remarks"></a>備註  
 所有類型的不可部份完成值傳遞至**min （)**必須是相同的基底類型的子類型。 接受的基底類型的類型，可支援**gt**作業。 這些類型包含三個內建數值基底類型以及日期/時間基底類型，它們是 xs:string、xs:boolean 以及 xdt:untypedAtomic。 xdt:untypedAtomic 類型的值會轉換為 xs:double。 如果沒有混用這些類型，或其他類型的其他值會傳遞，就會引發靜態錯誤。  
  
 結果**min （)**接收傳入的類型，例如 xdt 的 xs: double 類型的基底類型。 如果輸入是靜態空白，則會隱含空白並傳回靜態錯誤。  
  
 **Min （)**函式會傳回一個值小於輸入序列中的任何其他的順序。 對於 xs:string 值，會使用預設 Unicode 字碼指標定序。 如果 xdt: untypedatomic 值無法轉換成 xs: double，值會忽略輸入序列中*$arg*。 如果輸入是動態計算的空白序列，則會傳回空白序列。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. 使用 min() XQuery 函數尋找包含最少工時的工作中心位置  
 下列查詢擷取在製造產品型號 (ProductModelID=7) 的過程中，包含最少工時的所有工作中心位置。 一般而言，會傳回單一位置，如下所示。 如果有多個位置包含相等的最少工時數目，就會將它們全部傳回。  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  for   $Location in /AWMI:root/AWMI:Location  
  where $Location/@LaborHours =  
          min( /AWMI:root/AWMI:Location/@LaborHours )  
return  
  <Location WCID=     "{ $Location/@LocationID }"   
              LaborHrs= "{ $Location/@LaborHours }" />  
  ') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   **命名空間**關鍵字在 XQuery 初構中的定義的命名空間前置詞。 之後會在 XQuery 主體中使用前置詞。  
  
 XQuery 主體會建構 XML，\<位置 > 項目包含具有 WCID 與**LaborHrs**屬性。  
  
-   該查詢也會擷取 ProductModelID 與名稱值。  
  
 以下是結果：  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Min （)**函式會將所有整數都對應至 xs: decimal。  
  
-   **Min （)**不支援的 xs: duration 類型值的函數。  
  
-   不支援跨越基底類型界限的混合類型。  
  
-   不支援提供定序的語法選項。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
