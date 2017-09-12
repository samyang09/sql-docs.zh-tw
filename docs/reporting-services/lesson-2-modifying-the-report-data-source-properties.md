---
title: "第 2 課： 修改報表資料來源屬性 |Microsoft 文件"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be153d2ba1469034cad5e31e5e823d6ac5be4b4e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lesson 2: Modifying the Report Data Source Properties
在此 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 教學課程中，您將使用入口網站來選取傳遞給收件者的報表。 您將定義的資料驅動訂閱將散發 **建立基本資料表報表 &amp;#40;SSRS 教學課程&amp;#41;** 教學課程中建立的 [建立基本資料表報表 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)報表。  在下面的步驟中，您將修改報表用來取得資料的資料來源連接資訊。 只有使用 **預存認證** 來存取報表資料來源的報表可以透過資料驅動訂閱散發。 自動報表處理需要預存認證。  
  
您也會將資料集和報表修改成使用參數來依據 `[Order]` 篩選報表，讓訂閱能夠針對特定訂單和轉譯格式輸出不同的報表執行個體。  
  
## <a name="bkmk_modify_datasource"></a>修改資料來源以使用預存認證  
  
1.  以系統管理員權限瀏覽至 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 入口網站，例如以滑鼠右鍵按一下 Internet Explorer 的圖示，然後按一下 [以系統管理員​​身分執行​​]。  
 
2.    瀏覽至入口網站 URL。  例如：   
    `http://<server name>/reports`。  
    `http://localhost/reports`
 **注意：** web*入口網站*URL 為"Reports"，不報告*伺服器*"Reportserver"的 URL。  
3.  瀏覽到包含 **Sales Orders** 報表的資料夾，然後在報表的內容功能表中，按一下 **[管理]**。  
 
 ![ssrs_tutorial_datadriven_manage_report](../reporting-services/media/ssrs-tutorial-datadriven-manage-report.png)
  
3.  按一下**資料來源**的左窗格中。  
  
4.  確認**連線類型**是**Microsoft SQL Server**。  
  
5.  確認連接字串如下所示，並假設範例資料庫位於本機資料庫伺服器上：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
6.  按一下**使用以下認證**。  
  
7. 在**的認證類型**，選取**Windows 使用者名稱和密碼**
8. 輸入您的使用者名稱 (使用 *domain\user*格式) 和密碼。 如果您沒有存取 AdventureWorks2014 資料庫的權限，請指定有這項權限的登入。  
    
9. 按一下**測試連接**以確認您可以連接到資料來源。  
  
10. 按一下 **[儲存]**。
11. 按一下**取消**  
  
11. 檢視報表以確認報表是以您指定的認證來執行。 報表。  
  
## <a name="bkmk_modify_dataset"></a>若要修改 AdventureWorksDataset  
 在下列步驟中，您將修改資料集，以使用參數來根據訂單號碼篩選資料集。
1.  在下列位置開啟 **銷售訂單** 報表 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  以滑鼠右鍵按一下 `AdventureWorksDataset` 資料集，然後按一下 [資料集屬性]。  
    ![ssrs_tutorial_datadriven_datasetproperties](../reporting-services/media/ssrs-tutorial-datadriven-datasetproperties.png)  
3.  在 `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` 陳述式前面加入 `Group By` 陳述式。 完整的查詢語法如下：  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  按一下 **[確定]**。  
 在下列步驟中，您會將參數加入報表。  此報表參數會提供資料集參數。 
## <a name="bkmk_add_reportparameter"></a>若要加入報表參數並重新發行報表  
  
1.  在 [報表資料] 窗格中，展開 [參數] 資料夾，然後按兩下 **Ordernumber** 參數。  在上一個步驟中，當您將參數加入資料集時，系統會自動建立此參數。 按一下 [新增]，然後按一下 [參數...]  
 ![ssrs_tutorial_datadriven_parameter](../reporting-services/media/ssrs-tutorial-datadriven-parameter.png) 
2.  確認 [名稱] 是 `OrderNumber`。  
  
3.  確認**提示**是`OrderNumber`。  
  
4.  選取**允許空白值 ("")**。  
  
5.  選取**允許 null 值**。  
  
6.  按一下 **[確定]**。  
  
7.  按一下**預覽**來執行報表 索引標籤。 請注意，參數輸入方塊會出現在報表頂端。 您可以：  
  
    -   按一下 [檢視報表] 查看完整報表，而不使用參數。  
  
    -   取消選取 [Null] 選項並輸入訂單號碼 (例如 *so71949*)，然後按一下 [檢視報表]，即可單獨檢視報表中的單一訂單。  
    ![ssrs_tutorial_datadriven_reportviewer_parameter](../reporting-services/media/ssrs-tutorial-datadriven-reportviewer-parameter.png) 
 
  
## <a name="bkmk_redeploy"></a>重新部署報表  
  
1.  請重新部署報表，讓下一課的訂閱組態能夠運用您在這一課所做的變更。 如需有關用於資料表教學課程專案屬性的詳細資訊，請參閱 ' 將報表發行至報表伺服器 （選擇性）' 區段的[第 6 課： 加入群組和總計 &#40;Reporting Services &#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
2.  在工具列上，按一下 **[建置]** ，然後按一下 **[部署教學課程]**。  
  
## <a name="next-steps"></a>後續步驟  
+ 您已順利設定報表來利用預存認證取得資料，此資料可透過參數進行篩選。 
+ 在下一課，您將使用入口網站的 [資料驅動訂閱] 頁面來設定訂閱。 請參閱 [第 3 課：定義資料驅動訂閱](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)。  
  
## <a name="see-also"></a>另請參閱  
[管理報表資料來源](../reporting-services/report-data/manage-report-data-sources.md)  
[指定報表資料來源的認證及連接資訊](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
[建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[建立基本資料表報表 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  

