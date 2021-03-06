---
title: 硬體安裝 (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f612b9-f320-4391-952b-d3696cfbe2e2
caps.latest.revision: 17
ms.openlocfilehash: 24236e525efbc96c7e263a293f2a27582d700929
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="hardware-installation"></a>硬體安裝
本主題描述如何移動，請解除封裝，並安裝您的 SQL Server PDW 應用裝置的硬體。 本主題只是參考，並要幫助您了解程序。 應該解除封裝，安裝，而且您開啟之前，檢查您的應用裝置。 客戶參與是必要項目，例如資料中心存取、 電力和乙太網路連線。  
  
## <a name="BeforeMoving"></a>在您從裝貨碼頭移動任何元件之前  
移動、 解除封裝，或機架任何設備元件之前，請執行下列工作。  
  
|工作|Description|  
|--------|---------------|  
|請確認所有元件已都到達|若要確認已到達的所有元件，以及其在接收的停駐的您的資料中心的其他項目的上使用的用料表 (BOM)。|  
|確認資料中心符合該裝置的所有需求|這項工作一開始會檢閱硬體規格，並以您 IHV 提供纜線圖表。 後續步驟提供的具體說明機架空間與連線需求。|  
|確認資料中心有適當的機架空間|確認資料中心具有足夠空間可供所有設備的機架。<br /><br />請確認機架空間是空白且準備好接收設備的機架。|  
|請確認資料中心都符合連線需求|確認資料中心符合纜線圖表中的纜線需求。<br /><br />請確認將會有空間供所有纜線與電源線之後會 racked 應用裝置節點。|  
|確認停駐和機架之間樓層符合加權需求|請確認所有其他項目的和機架之間地板可支援應用裝置節點的加權，尤其是在資料中心的地板。<br /><br />如需有關每個元件的加權詳細，請連絡您的 IHV。|  
|安全資料中心的機架|安全資料中心備妥您的資料中心位置，例如地震皮帶地震容易出錯的地理區域中視需要使用額外的設備的機架。|  
|準備傳輸元件的協助|事先判斷哪些協助、 設備和工具，您需要處理每個元件，安全無虞地並不會導致損毀。|  
  
## <a name="Moving"></a>在資料中心，從裝貨碼頭移動機架  
每個棧板包含一個設備的機架，包括節點、 纜線、 線等的所有元件。  
  
您可以使用下列檢查清單，會將每個應用裝置機架從裝貨碼頭在棧板中的資料中心的機架位置。 首先，將控制項機架，然後再移 其他應用裝置資料機架。  
  
> [!WARNING]  
> 若要執行這些步驟所述完全失敗可能導致 bodily 損害，您的 SQL Server PDW 應用裝置或其他問題所造成的損害。  
>   
> 永遠不會嘗試以提起或移動應用裝置節點或其他大量的元件，而不需協助或合適的設備。 如需有關每個元件的加權詳細連絡您 IHV，好讓您在什麼協助、 設備和工具，您將需要安全無虞地並不會導致損毀處理每個元件可以事先判斷。  
  
|工作|Description|  
|--------|---------------|  
|請確認這個棧板層級|開始移動或解除封裝這個棧板之前，先確定其位於層級的接地。|  
|Unbolt 棧板中的節點|開始這個棧板的頂端，unbolt 從這個棧板最上層節點。|  
|將節點移到 dolly 或可支援加權的購物車|使用坡道提升和適當提起/移動技巧，將節點移到 dolly 或購物車可支援加權。|  
|在資料中心傳輸節點|使用適當的工作/移動技巧，將節點移至資料中心的機架中的位置。|  
|機架安全資料中心中的節點|機架安全資料中心中的位置中的節點。|  
|重複這些步驟的下一個節點或元件|重複上述步驟，將下一個節點或其他設備元件移到資料中心。|  
  
## <a name="AfterMoving"></a>安裝其他元件  
您可以使用下列檢查清單來安裝其他元件。  
  
|工作|Description||  
|--------|---------------|-|  
|解除封裝，並在網路交換器與多個 Pdu 機架|將網路交換器與多個 Pdu 機架中的適當位置中使用機架圖表。||  
|連接纜線標籤根據 Infiniband 和乙太網路纜線|請參閱纜線的圖表。 每個纜線兩端，指定連線需要有標籤。||  
|連接電源纜線|請參閱纜線的圖表。||  
|開啟機架並 Pdu 電源供應器|電源供應器機架和連接到 Pdu 機架中。 **請勿在這個階段電源上任何其他的應用裝置元件。**||  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
