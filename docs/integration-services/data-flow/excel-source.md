---
title: Excel 來源 | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6a9795de30c7d4fbe2ede9a17043a916e5953cd5
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="excel-source"></a>Excel 來源
  Excel 來源會從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿中的工作表或範圍擷取資料。  

> [!IMPORTANT]
> 如需連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)。

## <a name="access-mode"></a>存取模式
 Excel 來源會提供四種不同的資料存取模式來擷取資料：  
  
-   資料表或檢視。  
  
-   在變數中指定的資料表或檢視。  
  
-   SQL 陳述式的結果。 查詢可以是參數化查詢。  
  
-   儲存在變數中之 SQL 陳述式的結果。  
  
 Excel 來源會使用 Excel 連接管理員連接到資料來源，而連接管理員會指定要使用的活頁簿檔案。 如需詳細資訊，請參閱 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
 Excel 來源有一個一般輸出和一個錯誤輸出。  
  
## <a name="usage-considerations"></a>使用狀況的考量  
 Excel 連線管理員會使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支援的 Excel ISAM (Indexed Sequential Access Method，索引循序存取方法) 驅動程式，連接和讀寫資料至 Excel 資料來源。  
  
 許多現有的「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫」文件都有記錄此提供者和驅動程式的行為，而即使這些文件並非 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或其前置的「資料轉換服務」專用，您仍會想了解可能導致未預期結果的特定行為。 如需有關 Excel 驅動程式之使用與行為的一般資訊，請參閱＜ [如何從 Visual Basic 或 VBA 搭配使用 ADO 與 Excel 資料](http://support.microsoft.com/kb/257819)＞。  
  
 下列使用 Excel 驅動程式之 Jet 提供者的行為，在從 Excel 資料來源讀取資料時，可能導致未預期的結果。  
  
-   **資料來源**。 Excel 活頁簿中資料的來源可以是工作表 (必須附加 $ 符號，例如 Sheet1$) 或已命名的範圍 (例如 MyRange)。 在 SQL 陳述式中，工作表的名稱必須加以分隔 (例如 [Sheet1$])，以避免 $ 符號造成的語法錯誤。 「查詢產生器」會自動加入這些分隔符號。 當您指定工作表或範圍時，驅動程式會讀取連續的資料格區塊，從工作表或範圍左上角的第一個非空白資料格開始。 因此，來源資料的資料列不可以空白，或標題或標頭資料列與資料列之間不可以有空白資料列。  
  
-   **遺漏值**。 Excel 驅動程式會在指定來源中讀取特定資料列數目 (依預設為 8 個資料列)，以猜測各資料行的資料類型。 當資料行可能包含混合資料類型，尤其是數值資料與文字資料混合時，驅動程式會做出有利於大部分資料類型的決定，並於包含其他類型資料的資料格中傳回 Null 值。 (在繫結中，以數值類型優先)。Excel 工作表中大部分的資料格格式化選項，似乎都不會影響這項資料類型決定。 您可以藉由指定「匯入模式」來修改 Excel 驅動程式的這項行為。 若要指定「匯入模式」，請在 [屬性] 視窗中將 **IMEX=1** 加入 Excel 連線管理員之連接字串中的「擴充屬性」值。 如需詳細資訊，請參閱 [PRB: Excel Values Returned as NULL Using DAO OpenRecordset](http://support.microsoft.com/kb/194124) (PRB：使用 DAO OpenRecordset 以 NULL 形式傳回的 Excel 值)。  
  
-   **截斷的文字**。 當驅動程式判斷出某個 Excel 資料行包含文字資料時，驅動程式將會根據其取樣的最長值來選取資料類型 (字串或備忘錄)。 如果驅動程式未在其取樣的資料列中發現任何長度超過 255 個字元的值，則會將該資料行視為 255 個字元字串資料行而非備忘錄資料行 因此，長度超過 255 個字元的值可能會被截斷。 若要以不截斷的方式從備忘資料行匯入資料，您必須確保至少在其中一個取樣資料列中的備忘錄資料行包含長度超過 255 個字元的值，否則您就必須增加驅動程式取樣的資料列數目，使其包含這類資料列。 您可以提高 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** 登錄機碼底下 **TypeGuessRows** 的值，藉以增加取樣的資料列數目。 如需詳細資訊，請參閱 [PRB︰從 Jet 4.0 OLEDB 來源傳送資料失敗，發生緩衝區溢位錯誤](http://support.microsoft.com/kb/281517)(PRB: Transfer of Data from Jet 4.0 OLEDB Source Fails w/ Error)。  
  
-   **資料類型**。 Excel 驅動程式只能辨識有限的一組資料類型。 例如，所有的數值資料行都會被解譯為倍整數 (DT_R8)，而所有的字串資料行 (備忘錄資料行除外) 全都會被解譯成 255 個字元的 Unicode 字串 (DT_WSTR)。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 對應 Excel 資料類型的情況如下：  
  
    -   數值 – 雙精確度浮點數 (DT_R8)  
  
    -   貨幣 – 貨幣 (DT_CY)  
  
    -   布林值 – 布林值 (DT_BOOL)  
  
    -   日期/時間 – **datetime** (DT_DATE)  
  
    -   字串 – Unicode 字串，長度 255 (DT_WSTR)  
  
    -   備忘錄 – Unicode 文字資料流 (DT_NTEXT)  
  
-   **資料類型和長度轉換**： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不會隱含地轉換資料類型。 因此，您可能必須使用衍生的資料行轉換或資料轉換，在將 Excel 資料載入到非 Excel 目的地之前明確轉換 Excel 資料，或是在將非 Excel 資料載入到 Excel 目的地之前轉換資料。 在這種情況下，使用「匯入和匯出精靈」建立初始封裝可能很有用，因為這個精靈會為您設定必要的轉換。 某些轉換範例可能必須包含下列各項：  
  
    -   Unicode Excel 字串資料行與具有特定字碼頁之非 Unicode 字串資料行之間的轉換  
  
    -   255 個字元之 Excel 字串資料行與不同長度之字串資料行之間的轉換  
  
    -   雙精確度 Excel 數值資料行與其他類型之數值資料行之間的轉換  
  
## <a name="excel-source-configuration"></a>Excel 來源組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之所有屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 自訂屬性](../../integration-services/data-flow/excel-custom-properties.md)  
  
 如需循環使用 Excel 檔案群組的資訊，請參閱 [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [在資料流程元件中將查詢參數對應至變數](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [使用 Foreach 迴圈容器來執行 Excel 檔案和資料表迴圈](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
## <a name="excel-source-editor-connection-manager-page"></a>Excel 來源編輯器 (連接管理員頁面)
  使用 **[Excel 來源編輯器]** 對話方塊的 **[連接管理員]** 節點，以選取來源要使用的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿。 Excel 來源會從工作表或現有活頁簿的具名範圍中讀取資料。  
  
> [!NOTE]  
>  在 **[Excel 來源編輯器]** 中無法使用 Excel 來源的 **CommandTimeout**屬性，但可使用 **[進階編輯器]**來設定這個屬性。 如需有關這個屬性的詳細資訊，請參閱＜ [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)＞的＜Excel 來源＞一節。  
  
### <a name="static-options"></a>靜態選項  
 **[無快取]**  
 從清單中選取現有的 Excel 連線管理員，或按一下 [新增] 建立新的連線管理員。  
  
 **新增**  
 使用 [Excel 連線管理員] 對話方塊來建立新的連線管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|資料表或檢視|從工作表或 Excel 檔案的具名範圍中擷取資料。|  
|資料表名稱或檢視名稱變數|在變數中指定工作表或範圍名稱。<br /><br /> **相關資訊︰**[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL (命令)|使用 SQL 查詢從 Excel 檔案中擷取資料。 |  
|來自變數的 SQL 命令|在變數中指定 SQL 查詢文字。|  
  
 **預覽**  
 使用 [資料檢視] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
### <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
  
#### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **Excel 工作表的名稱**  
 從 Excel 活頁簿的可用工作表或具名範圍清單中，選取工作表或具名範圍的名稱。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 選取包含工作表名稱或具名範圍的變數。  
  
#### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢的文字，按一下 [建立查詢] 建立查詢，或按一下 [瀏覽] 瀏覽至包含查詢文字的檔案。  
  
 **參數**  
 如果您所輸入的參數化查詢使用 ? 做為查詢文字中的參數預留位置，請使用 **[設定查詢參數]** 對話方塊，將查詢輸入參數對應到封裝變數。  
  
 **建立查詢**  
 使用 [查詢產生器] 對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>資料存取模式 = 來自變數的 SQL 命令  
 **變數名稱**  
 選取包含 SQL 查詢文字的變數。  
  
## <a name="excel-source-editor-columns-page"></a>Excel 來源編輯器 (資料行頁面)
  使用 [Excel 來源編輯器] 對話方塊的 [資料行] 頁面，將輸出資料行對應至每個外部 (來源) 資料行。  
  
### <a name="options"></a>選項。  
 **可用的外部資料行**  
 在資料來源中檢視可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。  
  
 **[外部資料行]**  
 依工作讀取外部 (來源) 資料行的順序來檢視它們。 首先取消選取上述資料表中選取的資料行，然後依不同順序從清單中選取外部資料行，就可以變更此順序。  
  
 **輸出資料行**  
 為每個輸出資料行提供唯一的名稱。 預設值為選取的外部 (來源) 資料行的名稱；不過，您也可以選擇任何唯一的、描述性的名稱。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
## <a name="excel-source-editor-error-output-page"></a>Excel 來源編輯器 (錯誤輸出頁面)
  使用 [Excel 來源編輯器] 對話方塊的 [錯誤輸出] 頁面，以選取錯誤處理選項，並設定錯誤輸出資料行上的屬性。  
  
### <a name="options"></a>選項。  
 **輸入或輸出**  
 檢視資料來源的名稱。  
  
 **資料行**  
 檢視您在 [Excel 來源編輯器] 對話方塊的 [連線管理員] 頁面上所選取的外部 (來源) 資料行。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題** [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 指定截斷發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **說明**  
 檢視錯誤的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="related-content"></a>相關內容  
[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)
[Excel 目的地](excel-destination.md)  
[Excel 連線管理員](../connection-manager/excel-connection-manager.md)
