---
title: SQLExtendedFetch （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1d933ab2cbed3b79acee309459da1fb44a3e0f74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 層級 2  
  
 類似於[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)但傳回每個資料行使用陣列的多個資料列。 結果集是順向可捲動且可進行回溯可捲動資料指標定義為靜態，不是順如果。  
  
 根據預設，Visual FoxPro ODBC 驅動程式不會傳回資料列標示為 FoxPro 資料表中刪除。 標示為刪除但尚未從資料表移除資料列不會包含在結果集資料指標。 您可以使用來變更此行為[設定刪除](../../odbc/microsoft/set-deleted-command.md)命令。  
  
 如需詳細資訊，請參閱[SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md)中*ODBC 程式設計人員參考*。
