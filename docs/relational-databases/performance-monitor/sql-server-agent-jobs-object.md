---
title: "SQL Server Agent、Jobs 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f372eced96ca17d4fd547a11a56cfefd732394b9
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-agent-jobs-object"></a>SQL Server 代理程式、作業物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] SQL Server Agent 的 **Jobs** 效能物件包含效能計數器，用來報告 SQL Server Agent 作業的相關資訊。 下表列出這個物件包含的計數器。  
  
 下表包含 **SQLAgent:Jobs** 計數器。  
  
|[屬性]|描述|  
|----------|-----------------|  
|**Active Jobs**|此計數器報告目前執行中的作業數目。|  
|**Failed jobs**|此計數器報告因失敗而結束的作業數目。|  
|**Job success rate**|此計數器報告已順利完成的已執行作業百分比。|  
|**Jobs activated/minute**|此計數器報告在上一分鐘內啟動的作業數目。|  
|**Queued jobs**|此計數器報告備妥而可供 SQL Server Agent 執行，但尚未開始執行的作業數目。|  
|**Successful jobs**|此計數器報告因成功完成而結束的作業數目。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|執行個體|描述|  
|--------------|-----------------|  
|**_Total**|所有作業的資訊。|  
|**警示**|由警示啟動之作業的資訊。|  
|**其他**|不是由警示或排程啟動之作業的資訊。 一般而言，這些作業是手動使用 **sp_start_job**來啟動。|  
|**排程**|由排程啟動之作業的資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [實作作業](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [使用效能物件](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
