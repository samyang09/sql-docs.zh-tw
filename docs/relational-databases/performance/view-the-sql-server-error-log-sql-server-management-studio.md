---
title: "檢視 SQL Server 錯誤記錄檔 (SQL Server Management Studio) | Microsoft 文件"
ms.custom: 
ms.date: 07/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4acdc87a3317c38b5b19235dae681bce426244e3
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>檢視 SQL Server 錯誤記錄檔 (SQL Server Management Studio)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔包含使用者定義事件和特定系統事件，以用於進行疑難排解。 
  

  ## <a name="how-to-view-the-logs"></a>如何檢視記錄檔
1.  在 SSMS 中，選取物件總管

>**開啟** 物件總管：鍵盤快速鍵是 **F8**。 或者，在上層功能表上，按一下 [檢視]/物件總管 ![Object_explorer](../../relational-databases/performance/media/object-explorer.png) 


2.  在物件總管中，連接到 SQL Server 執行個體，然後展開該執行個體。
  
3.  尋找並展開 [管理] 區段 (假設您有權限可以看到它)。

4.  以滑鼠右鍵按一下 [SQL Server 記錄檔]，並選取 [檢視]，然後選擇 [檢視 SQL Server 記錄檔]。
 ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5.  將會出現記錄檔檢視器 (可能需要一分鐘)，內含可供您檢視的記錄檔清單。
  
6. 許多人都建議 [MSSQLTips.com](https://www.mssqltips.com/) 的有用文章： [Identify location of the SQL Server Error Log file](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/)(識別 SQL Server 錯誤記錄檔的位置)。 它們包含許多的絕佳資訊；請務必參閱！
  
  
