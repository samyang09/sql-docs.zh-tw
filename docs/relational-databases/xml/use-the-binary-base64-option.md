---
title: "使用 BINARY BASE64 選項 | Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e0761b3be2cd4148f972fb1dea488e38e725a85
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="use-the-binary-base64-option"></a>使用 BINARY BASE64 選項
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
若查詢中指定 BINARY BASE64 選項，就會以 Base64 編碼格式傳回二進位資料。 依預設，若沒有指定 BINARY BASE64 選項，則 AUTO 模式可支援 URL 編碼的二進位資料。 也就是說，不是傳回二進位資料，而是傳回一個參考，以指向查詢執行所在之資料庫虛擬根目錄的相對 URL。 此參考可用來存取後續作業中的實際二進位資料 (使用 SQLXML ISAPI dbobject 查詢)。 此查詢必須提供足夠的資訊 (例如：主索引鍵資料行)，以便識別影像。  
  
 在指定查詢時，若將別名用於檢視的二進位資料行，就會在 URL 編碼的二進位資料中傳回該別名。 在後續動作中該別名不具任何意義，且無法使用 URL 編碼來擷取影像。 所以在利用 FOR XML AUTO 模式查詢檢視時，請勿使用別名。  
  
 例如在 SELECT 查詢中，將任何資料行轉換為二進位大型物件 (BLOB)，會使其成為遺失關聯資料表名稱與資料行名稱的暫存實體。 而這會使得 AUTO 模式查詢產生錯誤，因為查詢不知道要將此值放入 XML 階層中的哪個位置。 例如：  
  
```  
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)  
INSERT INTO MyTable VALUES (1, 0x7);  
```  
  
 由於轉換為二進位大型物件 (BLOB)，因此查詢產生錯誤：  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO;  
```  
  
 解決方法是將 BINARY BASE64 選項加入 FOR XML 子句中。 若將轉換移除，則查詢會產生預期中的結果：  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO, BINARY BASE64;  
```  
  
 以下是結果：  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 AUTO 模式](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
