---
title: 監視記憶體最佳化的系統版本設定時態表 | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7a06785d-dbcb-44de-b95c-26b131471bee
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6199fab91f890a21bbdb94e138dfa4b28a8850b6
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="monitoring-memory-optimized-system-versioned-temporal-tables"></a>監視記憶體最佳化的系統建立版本時態表
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  針對每個系統建立版本的記憶體最佳化資料表，您可以使用現有的檢視來追蹤其詳細和摘要記憶體耗用量。  
  
 詳細的記憶體耗用量 (依據每個主要的系統建立版本和內部歷程記錄暫存表格分割)：  
  
```  
--Details of memory consumption   
WITH InMemoryTemporalTables   
AS   
(   
   SELECT SCHEMA_NAME ( T1.schema_id ) AS TemporalTableSchema  
      , T1.object_id AS TemporalTableObjectId  
      , IT.object_id AS InternalTableObjectId  
      , OBJECT_NAME ( IT.parent_object_id ) AS TemporalTableName  
      , IT.Name AS InternalHistoryStagingName   
   FROM sys.internal_tables IT    
   JOIN sys.tables T1 ON IT.parent_object_id = T1.object_id   
   WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2    
)   
  
SELECT   
     TemporalTableSchema  
   , T.TemporalTableName  
   , T.InternalHistoryStagingName,    
     CASE   
        WHEN C.object_id = T.TemporalTableObjectId   
        THEN 'Temporal Table Consumption'   
         ELSE 'Internal Table Consumption'   
         END ConsumedBy  
     , C.*   
   FROM sys.dm_db_xtp_memory_consumers C   
   JOIN InMemoryTemporalTables T   
      ON C.object_id = T.TemporalTableObjectId OR C.object_id = T.InternalTableObjectId   
   WHERE T.TemporalTableSchema = 'dbo' AND  T.TemporalTableName = 'FXCurrencyPairs' ;  
  
```  
  
 記憶體耗用量的摘要 (系統建立版本的記憶體最佳化資料表累加值)︰  
  
```  
--Summary of memory consumption   
WITH InMemoryTemporalTables   
AS   
(   
   SELECT SCHEMA_NAME ( T1.schema_id ) AS TemporalTableSchema  
     , T1.object_id AS TemporalTableObjectId  
     , IT.object_id AS InternalTableObjectId  
     , OBJECT_NAME ( IT.parent_object_id ) AS TemporalTableName  
     , IT.Name AS InternalHistoryStagingName   
   FROM sys.internal_tables IT    
   JOIN sys.tables T1 ON IT.parent_object_id = T1.object_id   
   WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2    
)   
, DetailedConsumption   
AS   
(   
   SELECT TemporalTableSchema  
      , T.TemporalTableName  
      , T.InternalHistoryStagingName  
      , CASE   
           WHEN C.object_id = T.TemporalTableObjectId   
           THEN 'Temporal Table Consumption'   
           ELSE 'Internal Table Consumption'   
           END ConsumedBy  
      , C.*   
    FROM sys.dm_db_xtp_memory_consumers C   
   JOIN InMemoryTemporalTables T   
      ON C.object_id = T.TemporalTableObjectId OR C.object_id = T.InternalTableObjectId   
)   
  
SELECT TemporalTableSchema  
     TemporalTableName  
   , sum ( allocated_bytes ) AS allocated_bytes  
   , sum ( used_bytes ) AS used_bytes   
FROM DetailedConsumption   
WHERE TemporalTableSchema = 'dbo' AND  TemporalTableName = 'FXCurrencyPairs'   
GROUP BY TemporalTableSchema, TemporalTableName ;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [建立記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [使用記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [記憶體最佳化系統版本設定時態表的效能考量](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
