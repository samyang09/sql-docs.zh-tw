---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb7b1eb95cd1b412368be74052af2a1cd2d9d145
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="localdberrortoomanysharedinstances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|287|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|共用的執行個體太多，無法產生唯一的使用者執行個體名稱。 請取消共用部分現有的共用執行個體。|  
  
## <a name="explanation"></a>說明  
 共用的執行個體太多，無法產生唯一的使用者執行個體名稱。  
  
## <a name="user-action"></a>使用者動作  
 請取消共用一個或多個共用的本機資料庫執行階段執行個體，然後再試一次。  
  
  
