---
title: "使用者定義資料類型 (UDT) 的 FOR XML 支援 | Microsoft Docs"
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
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c6b0369742c6432dfdf51f008eb95182518992a
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>使用者自訂資料類型 (UDT) 的 FOR XML 支援
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
FOR XML 不支援 Common Language Runtime (CLR) 使用者定義資料類型 (UDT)。  
  
 若要搭配 CLR 使用者定義資料類型使用 FOR XML，請確定此資料類型有 XML 序列化，並在 FOR XML SELECT 子句中使用 XML 的明確轉換。  
  
## <a name="see-also"></a>另請參閱  
 [各個 SQL Server 資料類型的 FOR XML 支援](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
