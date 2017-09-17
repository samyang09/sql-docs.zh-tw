---
title: "繫結資料行 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5903070b8918baa9734e5d188d90861322b57986
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="binding-columns"></a>繫結資料行
從資料來源提取的資料會傳回到應用程式已配置給此用途的變數中的應用程式。 作法是，應用程式必須產生關聯，或*繫結*，設定這些變數的結果資料行; 在概念上，此程序與應用程式變數繫結至陳述式參數相同。 當應用程式繫結至變數的結果集資料行時，它描述該變數，地址、 資料類型等 — 驅動程式。 驅動程式會將此資訊儲存在結構中，它會維持為該陳述式，並使用的資訊來從資料行傳回的值，在擷取資料列。  
  
 此章節包含下列主題。  
  
-   [繫結結果集資料行](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)