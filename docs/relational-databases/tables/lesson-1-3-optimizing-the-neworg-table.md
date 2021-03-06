---
title: 最佳化 NewOrg 資料表 | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39a6587d88d14f9ac1950f7e1f6896258860b452
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="lesson-1-3---optimizing-the-neworg-table"></a>第 1-3 課：最佳化 NewOrg 資料表
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
您在 **使用現有的階層式資料填入資料表** 工作中建立的 [NewOrd](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) 資料表包含所有員工資訊，並使用 **hierarchyid** 資料類型代表階層式結構。 此工作會新增索引以支援在 **hierarchyid** 資料行上進行搜尋。  
  
## <a name="clustered-index"></a>叢集索引  
**hierarchyid** 資料行 (**OrgNode**) 是 **NewOrg** 資料表的主要索引鍵。 建立資料表時，它包含名為 **PK_NewOrg_OrgNode** 的叢集索引以強制 **OrgNode** 資料行的唯一性。 此叢集索引也支援深度優先的資料表搜尋。  
  
## <a name="nonclustered-index"></a>非叢集索引  
此步驟會建立兩個非叢集索引來支援一般搜尋。  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>建立 NewOrg 資料表的索引以便進行有效率的搜尋  
  
1.  為協助在階層的相同層級進行查詢，使用 [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) 方法來建立階層中包含層級的計算資料行。 然後，在層級和 **Hierarchyid**上建立複合式索引。 執行下列程式碼以建立計算資料行和廣度優先的索引：  
  
    ```  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  在 **EmployeeID** 資料行上建立唯一的索引。 這是依 **EmployeeID** 號碼之單一員工的傳統單一查閱。 執行下列程式碼，在 **EmployeeID**上建立索引：  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  執行下列程式碼，以全部三個索引的順序，從資料表擷取資料：  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  比較結果集以查看每個索引類型中儲存的順序。 只有每個輸出的前四個資料列遵照這個順序。  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    深度優先索引：員工記錄緊接著其主管儲存。  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    **EmployeeID** 優先索引：資料列會以 **EmployeeID** 順序儲存。  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> 如需顯示深度優先索引與廣度優先索引間差異的圖表，請參閱[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)。  
  
#### <a name="to-drop-the-unnecessary-columns"></a>卸除不必要的資料行  
  
1.  **ManagerID** 資料行代表員工/主管的關聯性，此種關聯性現在以 **OrgNode** 資料行代表。 如果其他應用程式不需要 **ManagerID** 資料行，請考慮使用下列陳述式卸除該資料行：  
  
    ```  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  **EmployeeID** 資料行也是多餘的。 **OrgNode** 資料行可唯一識別每個員工。 如果其他應用程式不需要 **EmployeeID** 資料行，請考慮使用下列程式碼先卸除索引，再卸除該資料行：  
  
    ```  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>以新的資料表取代原始的資料表  
  
1.  如果您的原始資料表包含任何額外的索引或條件約束，請將它們新增到 **NewOrg** 資料表中。  
  
2.  以新的資料表取代舊的 **EmployeeDemo** 資料表。 執行下列程式碼卸除舊的資料表，然後以舊名稱重新命名新的資料表：  
  
    ```  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  執行下列程式碼檢查最終的資料表：  
  
    ```  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[摘要：將資料表轉換為階層式結構](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
  
