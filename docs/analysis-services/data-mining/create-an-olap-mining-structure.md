---
title: "建立 OLAP 採礦結構 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21cbdc9d-d33c-4026-b9ef-1be2bd92b3b1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4c361d8a255b4ef5dc348692bb688a0421b0abd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-an-olap-mining-structure"></a>建立 OLAP 採礦結構
  建立以 OLAP Cube 或其他多維度資料存放區為根據的資料採礦模型有許多優點。 OLAP 方案已經包含妥善組織、清理和適當格式化的大量資料，但是這種資料的複雜性在於使用者不太可能根據隨選探索找到有意義的模式。 資料採礦讓您能夠探索新的相互關聯性，並提供可採取動作的洞察力。  
  
 本主題描述如何根據現有多維度方案中的維度和相關量值來建立 OLAP 採礦結構。  
  
 [需求](#bkmk_Reqs)  
  
 [OLAP 資料採礦處理概觀](#bkmk_Overview)  
  
 [在 OLAP 方案中使用資料採礦的案例](#bkmk_OLAP_Scenarios)  
  
 [篩選](#bkmk_Filters)  
  
 [使用巢狀資料表](#bkmk_Nested)  
  
 [資料採礦維度](#bkmk_DMDimension)  
  
##  <a name="bkmk_Reqs"></a> OLAP 採礦結構和模型的需求  
 如果您正在設計 OLAP 採礦模型，您的資料來源會已經存在於之前用來建立 Cube 的資料庫中。 您不能連接到遠端 Cube 及建立資料採礦物件；這些 Cube 物件必須存在於與您即將建立之採礦結構的資料庫相同的方案中。  
  
 如果您沒有原始專案檔或者不想要加以改變，您可以使用 Visual Studio 中的 [從伺服器匯入 (多維度和資料採礦)] 選項，取得中繼資料和方案物件的複本。 然後您可以修改部署目標、編輯資料來源，以及在不影響現有物件的情況下處理 Cube 物件。  
  
 如需詳細資訊，請參閱 [使用 Analysis Services 匯入精靈匯入資料採礦專案](../../analysis-services/data-mining/import-a-data-mining-project-using-the-analysis-services-import-wizard.md)。  
  
##  <a name="bkmk_Overview"></a> OLAP 資料採礦處理概觀  
 在方案總管中，以滑鼠右鍵按一下 [採礦結構] 節點，然後選取 [新增採礦結構]，即可啟動 [資料採礦精靈]。 此精靈會引導您透過下列步驟來建立新結構和模型的結構：  
  
1.  **選取定義方法**：您可以在這裡選取資料來源類型，並選擇 **[從現有的 Cube]**。  
  
    > [!NOTE]  
    >  當做來源使用的 OLAP Cube 必須存在於與採礦結構相同的資料庫中，如上面所述。 此外，您無法使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 增益集建立的 Cube 作為資料採礦的來源。  
  
2.  **建立資料採礦結構**：決定只要建立結構，還是建立包含採礦模型的結構。  
  
     您也必須選擇適當的演算法來分析資料。 如需哪一個演算法最適合某些工作的指示，請參閱＜資料採礦演算法 (Analysis Services - 資料採礦)＞。  
  
3.  **選取來源 Cube 維度**：這個步驟與選取資料來源相同。 您需要選擇單一維度，其中包含用於定型模型的最重要資料。 您之後可以加入其他維度的資料，或是篩選維度。  
  
4.  **選取案例索引鍵**：在您剛才選取的維度中，選擇一個屬性 (資料行) 當作案例資料的唯一識別碼。  
  
     通常系統會為您預先選取一個資料行，但如果實際上有多個索引鍵，您可以變更該資料行。  
  
5.  **選取案例層級資料行**：在這裡可以選擇選定維度中的屬性，以及與您的分析相關的相關量值。 這個步驟相當於從資料表選取資料行。  
  
     此精靈會自動包含之前使用選定維度中之屬性所建立的任何量值供您檢閱和選擇。  
  
     例如，如果您的 Cube 包含的量值會根據客戶的地理位置計算運費成本，而且您選擇「客戶」維度當做模型化的主要資料來源，則此量值將會被提議為候選項目加入至模型中。 請注意，不要加入已經直接根據屬性的太多量值，因為資料行之間已經有一個隱含的關聯性 (如量值公式中所定義)，而且這個預期的相互關聯性強度可能會隱蔽您可能發現的其他關聯性。  
  
6.  **指定採礦模型資料行使用方式**：對於您已加入至結構中的每一個屬性或量值而言，您都必須指定該屬性應該用於預測還是當做輸入使用。 如果您未選取任何選項，則會處理資料，但是不會將資料用於分析；但是，如果您之後啟用鑽研，這些資料可當做背景資料使用。  
  
7.  **加入巢狀資料表**：按一下可加入相關資料表。 在 **[選取量值群組維度]** 對話方塊中，可以從與目前維度相關的多個維度中選擇單一維度。  
  
     接下來，您可使用 **[選取巢狀資料表索引鍵]** 對話方塊，定義新的維度如何與包含案例資料的維度產生關聯。  
  
     使用 **[選取巢狀資料表資料行]** 對話方塊，從您想要用於分析的新維度中選擇屬性和量值。 您也必須指定巢狀屬性是否會用於預測。  
  
     在您加入可能需要的所有巢狀屬性之後，請回到 **[指定採礦模型資料行使用方式]**頁面，並按 **[下一步]**。  
  
8.  **指定資料行的內容和資料類型**：現在您已經加入將用於分析的所有資料，而且您必須針對每一個屬性指定 *「資料類型」* 和 *「內容類型」* 。  
  
     在 OLAP 模型中，您沒有自動偵測資料類型的選項，因為多維度方案已經定義資料類型，而且無法變更。 也會自動識別索引鍵。 如需詳細資訊，請參閱[資料類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/data-types-data-mining.md)。  
  
     您針對模型中所使用之每一個資料行所選擇的 *「內容類型」* 會告訴演算法應該如何處理資料。 如需詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
9. **配量來源 Cube**：在這裡可以定義 Cube 中的篩選，只選取某個資料子集並定型更有目標性的模型。  
  
     您可以篩選 Cube，方法是選擇篩選所依據的維度、選取包含您想要使用之準則的階層層級，然後輸入條件當做篩選條件使用。  
  
10. **建立測試集**：您可以在這個頁面上告訴精靈，應該將多少資料數量保留給測試模型使用。 如果您的資料將支援多個模型，則建立鑑效組資料集是一個很好的作法，這樣可以針對相同的資料測試所有模型。  
  
     如需詳細資訊，請參閱[測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)。  
  
11. **正在完成精靈**：在這個頁面上，您可以為新的採礦結構和關聯的採礦模型提供名稱，並儲存此結構和模型。  
  
     在此頁面上，您也可以設定下列選項：  
  
    -   **允許使用鑽研**  
  
    -   **建立採礦模型維度**  
  
    -   **使用採礦模型維度建立 Cube**  
  
     若要深入了解這些選項，請參閱本主題稍後的＜ [了解資料採礦維度和鑽研](#bkmk_DMDimension)＞章節。  
  
 此時，採礦結構和其模型都只是中繼資料，您需要加以處理才能得到結果。  
  
##  <a name="bkmk_OLAP_Scenarios"></a> 搭配 OLAP 資料使用資料採礦的案例  
 OLAP Cube 經常包含很多成員和維度，導致難以得知開始進行資料採礦的位置。 為了協助識別 Cube 所包含的模式，您通常會識別重要的單一維度，然後再開始探索與該維度相關的模式。 下表會列出數個常見的 OLAP 資料採礦工作，描述您可套用每個工作的範例狀況，並識別用於每一個工作的資料採礦演算法。  
  
|工作|範例狀況|演算法|  
|----------|---------------------|---------------|  
|將成員組成群集|依據客戶成員屬性、客戶購買的產品和客戶花費的金額，來分割客戶維度。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法|  
|尋找特別的或異常的成員|依據銷售量、收益、商店位置和商店大小，在商店維度中識別特別的或異常的商店。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法|  
|尋找特別的或異常的資料格|識別一段時間內與典型趨勢相反的商店銷售。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法|  
|尋找相互關聯|識別與伺服器停機時間相關的因素，包括區域、機器類型、作業系統或購買日期。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法|  
  
##  <a name="bkmk_Filters"></a>配量 Cube 與。篩選模型的比較  
 當您建立模型時配量 Cube 就像是在關聯式採礦模型上建立篩選。 在關聯式模型中，資料來源上的篩選會定義為 SQL 陳述式上的 WHERE 子句；在 Cube 中，您可使用編輯器來建立使用 MDX 的篩選陳述式。  
  
 例如，Cube 可能包含有關全球產品購買的資訊，但是在您的行銷活動中，您想要根據居住在英國地區且年齡 30 歲以上的女性客戶分析來建立模型。  
  
 在這個案例中，您將建立兩個篩選：  
  
-   在第一個篩選中，您會依序選擇「地理位置」維度和「區域」的階層，然後使用 [篩選運算式] 清單，從可能的值當中選擇「英國」。  
  
-   在第二個篩選中，您會選擇「客戶」維度，選取「性別」屬性，然後從屬性值清單中選取「女性」。  
  
 在建立採礦結構之後，您可以修改 Cube 資料的定義和篩選準則。 如需詳細資訊，請參閱[採礦模型的篩選](~/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
 **[採礦結構]** 索引標籤和 **[採礦模型]** 索引標籤會提供將篩選加入至現有採礦結構的選項，加入的方法是按一下 **[定義 Cube 配量]**。 **[配量 Cube]** 對話方塊會幫助您從下拉式清單中選擇值來建立有效的 MDX 篩選運算式。  
  
> [!WARNING]  
>  請注意， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中已經變更設計和瀏覽 Cube 的介面。 如需詳細資訊，請參閱 [瀏覽 Cube 中的資料和中繼資料](../../analysis-services/multidimensional-models/browse-data-and-metadata-in-cube.md)。  
  
 您可以在 Cube 上加入要傳回採礦模型所需資料之必要數量的篩選。 您也可以在個別 Cube 配量上定義配量。 例如，若結構包含兩個以產品為基礎的巢狀資料表，您可以在 2004 年 3 月配量一個資料表，並在 2004 年 4 月配量另一個資料表。 接著您可以使用所產生的模型，依據 3 月的購買來預測 4 月的購買。  
  
##  <a name="bkmk_Nested"></a> 在 OLAP 採礦模型中使用巢狀資料表  
 當您使用資料採礦精靈來建立以 Cube 資料為根據的模型時，您可以加入巢狀資料表，加入的方式是指定相關維度的名稱，然後選擇要加入至模型中的屬性或量值。  
  
 例如，如果案例資料所使用的主要維度為「客戶」，您可能會將相關維度當作「產品」維度加入，因為您預期客戶在一段期間內可能已訂購多個產品，而且此 Cube 已經透過訂單事實資料表將每一個客戶連結到多個產品。  
  
 您可在精靈的 **[指定採礦模型資料行使用方式]** 頁面上，按一下 **[加入巢狀資料表]**來加入巢狀資料表。 隨即開啟一個對話方塊，引導您選擇相關維度及任何量值的程序。 案例和巢狀維度必須與外部索引鍵相關，而且量值必須使用案例或巢狀資料表中已經包含的其中一個屬性。 不幸的是，這些限制對於縮小範圍並沒有很大的用處，所以您必須謹慎來選取只對模型化有用處的屬性。  
  
 對於您加入至巢狀資料表的每一個屬性或量值而言，您都必須指定巢狀屬性是否將用於預測，其方法是在 **[選取巢狀資料表資料行]** 對話方塊中選取 **[可預測]** 或 **[輸入]** 。 如果您未選取任何選項，該資料將會加入至採礦結構，但是不會用於分析。  
  
 對於每一個屬性和量值而言，您也必須指定此屬性為離散的、已離散化或是連續的。 此精靈會根據屬性的資料類型預先選取預設值，但是您可能需要根據演算法需求來加以變更。 如果您選擇的內容類型與您選擇的演算法不相容 (例如，您搭配貝氏機率分類模型使用連續數值類型)，您要等到嘗試處理模型之後才會得到錯誤訊息。  
  
 當您完成這些選項的設定之後，此精靈會將巢狀資料表加入至案例資料表。 巢狀資料表的預設名稱為巢狀維度的名稱，但您可以重新命名巢狀資料表和其資料行。 您可以重複此程序，將多個巢狀資料表加入至採礦結構。  
  
 能夠以這樣的方式使用巢狀資料表資料是 SQL Server 資料採礦的一項功能，此功能特別強大，而且在 Cube 中，使用相關資料子集的機率幾乎沒有限制。  
  
##  <a name="bkmk_DMDimension"></a> 了解資料採礦維度和鑽研  
 **[允許使用鑽研]**選項可讓您針對基礎 Cube 資料執行查詢，同時讓您瀏覽模型。 該資料不會包含在新的資料採礦維度中，但是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫可以使用資料繫結來擷取來源 Cube 中的資訊。  
  
 **[建立採礦模型維度]**選項可讓您在現有的 Cube 中產生新的維度，該維度包含演算法所發現的模式。 新維度中的階層大部分是由模型類型所決定。 例如，叢集模型的表示法相當平面，階層的頂端有 (全部) 節點，而每一個叢集會在下一層。 相反地，為決策樹模型建立的維度可能會有非常深入的階層，表示樹狀結構的分支。  
  
 **[使用採礦模型維度建立 Cube]**選項可讓您將新的資料採礦維度匯出到新的 Cube 中。 在資料採礦維度上鑽研所需的任何物件都會自動併入。  
  
> [!WARNING]  
>  只有以下的模型類型才支援資料採礦維度的建立：以 Microsoft 叢集演算法、Microsoft 決策樹演算法或 Microsoft 關聯演算法為根據的模型。  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦結構資料行](../../analysis-services/data-mining/mining-structure-columns.md)   
 [採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)   
 [採礦模型屬性](../../analysis-services/data-mining/mining-model-properties.md)   
 [採礦結構和結構資料行的屬性](../../analysis-services/data-mining/properties-for-mining-structure-and-structure-columns.md)  
  
  
