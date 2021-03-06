---
title: SQL Server Agent 屬性 (記錄頁面) | Microsoft Docs
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
- sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0da07d6c02c070f4819b2fd5758755992aa9c71d
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server Agent 屬性 (記錄頁面)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面來檢視和修改管理 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務記錄的設定。  
  
## <a name="options"></a>選項。  
**限制作業記錄大小**  
對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 在記錄中所保留的作業記錄資訊量加以設限。  
  
**作業記錄大小上限 (以資料列為單位)**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會保留的最大資料列數目。 當記錄成長至此資料列數目時，隨著新資料列的輸入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會移除記錄中最舊的資料列。  
  
**每項作業的作業記錄最大資料列數**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會為每項作業保留的最大資料列數目。 當特定作業的記錄成長至此資料列數目時，隨著新資料列的輸入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會移除記錄中最舊的資料列。  
  
**移除代理程式記錄**  
指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會移除已存在於記錄中超過指定時間長度的項目。 這是單次移除記錄的執行作業。 如果需要重複的作業，請建立並排程含有清除作業的維護計畫。  
  
**早於**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會保留項目的時間。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Agent 錯誤記錄檔](../../ssms/agent/sql-server-agent-error-log.md)  
  
