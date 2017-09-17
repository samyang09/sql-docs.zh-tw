---
title: "RDS 傳回&quot;資料流不讀取&quot;錯誤 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5c0cbc0d8c83a2d36fc931616046b0261938a0a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS 傳回&quot;資料流不讀取&quot;錯誤
「 資料流物件無法讀取，因為它是空的或目前的位置位於資料流結尾。 對於非空白的資料流，設定 Position 屬性與目前的位置。 若要判斷是否為空資料流，檢查 [大小] 屬性。 」  
  
 如果您看到此錯誤訊息，您可能會嘗試透過 http 使用參數化的階層式查詢。 RDS 不允許您使用遠端參數化的階層。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


