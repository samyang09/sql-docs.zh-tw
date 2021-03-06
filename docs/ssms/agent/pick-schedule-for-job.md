---
title: 作業的挑選排程 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cbae4854bff8396f64e04a662d0e2b48548934b7
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="pick-schedule-for-job"></a>作業的挑選排程
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此對話方塊即可挑選 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業的現有排程。  
  
## <a name="options"></a>選項。  
**可用的排程**  
列出此作業可用的排程。 因為作業和排程必須有相同的擁有者，所以此清單只會包含工作擁有者所擁有的排程。  
  
**名稱**  
顯示排程名稱。  
  
**已啟用**  
選取是否啟用排程。  
  
**說明**  
描述排程執行作業所用的條件。  
  
**排程中的作業**  
列出附加至排程的作業編號。 按一下某個編號以檢視該作業的屬性。  
  
**屬性**  
啟動 [作業排程屬性] 對話方塊，您可以在其中檢視排程的相關資訊。  
  
## <a name="see-also"></a>另請參閱  
[建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
  
