---
title: dbo.sysschedules (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysjobschedules
- dbo.sysjobschedules
- dbo.sysjobschedules_TSQL
- sysjobschedules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobschedules system table
ms.assetid: ccdafec7-2a9b-4356-bffb-1caa3a12db59
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 894bf5f590724b4a044dbcf960e99799d5724c09
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要執行之作業的排程資訊。 這份資料表儲存在**msdb**資料庫。  
  
> **注意：** **sysjobschedules**資料表重新整理每隔 20 分鐘，這可能會影響傳回的值**sp_help_jobschedule**預存程序。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|排程的識別碼。|  
|**job_id**|**uniqueidentifier**|作業的識別碼。|  
|**next_run_date**|**int**|排程下一次執行作業的日期。 日期格式為 YYYYMMDD。|  
|**next_run_time**|**int**|排程執行作業的時間。 時間格式為 HHMMSS，使用 24 小時制。|  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysjobschedules &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
