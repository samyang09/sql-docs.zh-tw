---
title: Always On 可用性群組等候類型 (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: afa8caff-f325-48d9-a8ef-a30beab60389
caps.latest.revision: 6
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: d05f65155310f80778d1697d6d4a1a0188796fde
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="always-on-availability-groups-wait-types"></a>Always On 可用性群組等候類型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  當您在針對 Always On 可用性群組延遲進行疑難排解時，可以使用動態管理檢視 (DMV) [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) 中的可用性群組特定等候類型，來監視等候的統計資料的累積。  
  
 如需使用等候統計資料的一般資訊，請參閱 [SQL Server 2005 等候和佇列](https://technet.microsoft.com/library/cc966413.aspx) \(英文\)。 該文件是針對 SQL Server 2005 撰寫，但其資訊可以套用到更新的 SQL Server 版本。  
  
## <a name="query-for-availability-groups-wait-types"></a>查詢可用性群組等候類型  
 使用以下 T-SQL 查詢來擷取具有可用性群組等候類型的所有等候的統計資料：  
  
```sql  
SELECT * FROM sys.dm_os_wait_stats   
WHERE wait_type LIKE '%hadr%'  
ORDER BY wait_time_ms DESC  
```  
  
 若要藉由擷取擴充事件來監視等候的統計資料，請使用以下 T-SQL 命令。  
  
```sql
CREATE EVENT SESSION [alwayson] ON SERVER   
ADD EVENT sqlos.wait_info(  
    WHERE ([wait_type]=(758) OR [wait_type]=(776) OR [wait_type]=(853) OR [wait_type]=(833)))  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,  
MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)  
GO  
```  
  
 您可以執行以下查詢來檢視等候類型的索引鍵/值對應：  
  
```sql
SELECT * FROM sys.dm_xe_map_values   
WHERE name='wait_types' AND map_value LIKE '%hadr%'   
ORDER BY map_key ASC  
```  
  
## <a name="next-steps"></a>後續步驟  
 [等候的類型](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md#WaitTypes)  
  
  