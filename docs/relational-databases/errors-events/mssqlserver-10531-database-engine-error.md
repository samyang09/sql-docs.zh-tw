---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85d3fc36300ef8e11b8114ad53435affea01d777
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10531"></a>MSSQLSERVER_10531
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10531|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_NO_ELIGIBLE_STMT|  
|訊息文字|無法從快取建立計畫指南 '%.*ls'，因為使用者沒有所需的權限。 請將 VIEW SERVER STATE 權限授予建立計畫指南的使用者。|  
  
## <a name="explanation"></a>說明  
使用者沒有足夠的權限，無法從計畫快取建立指定的計畫指南。  
  
## <a name="user-action"></a>使用者動作  
請將 VIEW SERVER STATE 權限授予建立計畫指南的使用者。  
  
## <a name="see-also"></a>另請參閱  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
