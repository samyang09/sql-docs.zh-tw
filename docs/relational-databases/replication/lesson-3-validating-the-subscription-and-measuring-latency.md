---
title: 第 3 課：驗證訂閱及測量延遲 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ad3fadb0017628fa54a102366f132bbc72b9cfb
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2018
---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>第 3 課：驗證訂閱及測量延遲
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在這一課，您將使用追蹤 Token，以確認變更正複寫至訂閱者，並決定延遲 (亦即在「發行者」端所做變更顯示在「訂閱者」上所花費的時間)。 您必須先完成上一課 [第 2 課：建立交易式發行集的訂閱](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md)，才能進行這一課。  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>插入追蹤 Token 並檢視 Token 上的資訊  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的「發行者」，展開伺服器節點，再以滑鼠右鍵按一下 [複寫] 資料夾，然後按一下 [啟動複寫監視器]。  
  
    複寫監視器隨即啟動。  
  
2.  在左窗格中展開「發行者」群組，展開「發行者」執行個體，然後按一下 **AdvWorksProductTrans** 發行集。  
  
3.  按一下 **[追蹤 Token]** 索引標籤。  
  
4.  按一下 **[插入追蹤]**。  
  
5.  在下列資料行中檢視追蹤 Token 的經過時間： **[發行者到散發者]**、 **[散發者到訂閱者]**、 **[延遲總計]**。 **[暫止]** 表示 Token 尚未到達給定點。  
  
## <a name="next-steps"></a>Next Steps  
在這一課，您已順利使用追蹤 Token，驗證資料變更正從「發行者」複寫至「訂閱者」。 您也可以在「發行者」端插入、更新或刪除 **Product** 資料表中的資料，並在複寫之後，在「訂閱者」端查詢 **Product** 資料表，檢視這些變更。  
  
如此即已完成＜在連續連接的伺服器之間複寫資料＞教學課程。 如需使用合併式複寫的類似教學課程，請參閱 [教學課程：利用行動用戶端複寫資料](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)。  
  
## <a name="see-also"></a>另請參閱  
[針對異動複寫測量延遲及驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
  
