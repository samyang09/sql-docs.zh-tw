---
title: "從 SQL Server 2005 升級嗎？ | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ad40e66f-71fe-4ee6-9ce3-17127e7b1d7a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d582d7d9ca0bc90ca40ee34e946d49bf545024bd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>從 SQL Server 2005 升級嗎？

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 由於對 SQL Server 2005 的延伸支援即將結束，因此建議您立即升級到新版 SQL Server 及 Azure SQL Database。 透過升級，您能夠維護安全性與相容性、達到突破性的效能，並將資料平台基礎結構最佳化。  
  
 如需詳細資訊、指引及取得工具以規劃及自動化您的升級或移轉，請參閱 [不再支援 SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)。  
  
## <a name="why-upgrade"></a>為何要升級？  
  
> [!IMPORTANT]  
>  SQL Server 2005 的延長支援已於 2016 年 4 月 12 日結束。 如果您在 2016 年 4 月 12 日之後繼續執行 SQL Server 2005，則不會再收到任何安全性更新。  
  
## <a name="choose-your-upgrade-option"></a>選擇升級選項  
若要升級 SQL Server 2005 的關聯式資料庫，以下是 Microsoft 平台所提供的關聯式儲存體選項。  
  
若要查看這些選項更全面的分析，請 [按一下這裡](http://sql05upgrade.azurewebsites.net/)。  
  
|關聯式儲存體選項|優點|其他考量因素|  
|-------------------------------|--------------|-------------------------------|  
|**內部部署 SQL Server**<br /><br /> 此選項適用於任何種類 (從交易系統到資料倉儲) 的應用程式。|因為軟硬體皆由您所管理，所以您幾乎能自由操控各項功能與規模調整功能。<br /><br /> 若要從 SQL Server 2005 升級，這是最相似的環境。|因為您必須購買、維護及管理您所擁有的硬體與軟體，所以此選項的初期投資最高，管理時間也最長。<br /><br /> 如需詳細資訊，請參閱 [SQL Server](https://www.microsoft.com/EN-US/server-cloud/products/sql-server-2017/)。|  
|**裝載於 Azure 虛擬機器上的 SQL Server**<br /><br /> 您若希望享有下列便利，可考慮此選項：<br /><br /> 移轉到託管環境的優點。<br /><br /> 控制作業環境。<br /><br /> 使用熟悉 SQL Server 功能集。|您可以快速從虛擬機器的映像庫快速進行部署。<br /><br /> 您可以使用完整的 SQL Server 功能集。<br /><br /> 您可以節省在伺服器軟硬體上的投資。 您只需按每小時的使用量付費。|您必須設定及管理 SQL Server 與作業系統軟體。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)。<br /><br /> 如需移轉的相關資訊，請參閱 [將資料庫移轉至 Azure VM 上的 SQL Server](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/)。|  
|**裝載 Azure SQL Database 的資料庫服務**<br /><br /> 若您需要價格較低、維護工作較少的解決方案，可以考慮此選項。<br /><br /> 此選項特別適合不需要時時保有相同容量的應用程式，或需要提供外部存取的應用程式。|您可以快速部署及相應增加。<br /><br /> 您只需按每小時的使用量付費。<br /><br /> 服務的費用不只有儲存體而已，還包括高可用性及自動化備份。|Azure SQL Database 所缺少的一些 SQL Server 功能並不適用於託管的雲端環境。 如需詳細資訊，請參閱 [Azure SQL Database Transact-SQL 資訊](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/)。<br /><br /> 相較於 SQL Server 的 524 PB，Azure SQL Database 的資料庫大小上限為 500 GB。<br /><br /> 如需詳細資訊，請參閱 [SQL Database](https://azure.microsoft.com/services/sql-database/)。<br /><br /> 如需移轉的相關資訊，請參閱 [將 SQL Server Database 移轉到 Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/)。|  
  
 對於某些資料及應用程式，您也可考慮使用非關聯式或 NoSQL 解決方案。  
  
|非關聯式解決方案|優點|  
|------------------------------|--------------|  
|**Azure Cosmos DB**<br /><br /> 您的現代化應用程式、可調式應用程式、行動應用程式及 Web 應用程式若是使用 JSON 資料，並需要兼具主動式查詢及交易式資料處理的功能，可以考慮此選項。<br /><br /> 如需詳細資訊，請參閱 [Cosmos DB](http://azure.microsoft.com/services/cosmos-db/)。<br /><br /> 如需匯入資料的資訊，請參閱[將資料匯入 Cosmos DB](http://docs.microsoft.com/azure/cosmos-db/import-data/)。|您的文件會編製索引，讓您可以使用熟悉的 SQL 語法加以查詢。<br /><br /> 資料庫無須設定結構描述。<br /><br /> 您無須重建索引，就可將屬性加入文件中。<br /><br /> 資料庫引擎內就能直接提供您 JSON 及 JavaScript 支援。<br /><br /> 除可獲得地理空間資料的原生支援之外，還可與其他 Azure 服務整合，包括 Azure 搜尋、HDInsight 及資料 Factory。<br /><br /> 專用的輸送量層級讓儲存體能有低延遲、高效能的表現。|  
|**Azure 資料表儲存體**<br /><br /> 若您需要價格實惠的解決方案來儲存以 PB 計的半結構化資料，可以考慮此選項。<br /><br /> 如需詳細資訊，請參閱 [資料表儲存體](https://azure.microsoft.com/services/storage/tables/)。|您無須將資料下線，就能持續改進您的應用程式與資料表結構描述。<br /><br /> 您無須分區化您的資料集，就能相應增加規模。<br /><br /> 異地備援支援可將您的資料複寫到多個區域。|  
  
## <a name="plan-your-upgrade"></a>規劃升級  
  
-   透過以下來自 SQL Server 小組的一系列部落格文章，了解如何計劃您的升級。  
  
    -   [Planning an efficient upgrade from SQL Server 2005: Step 1 of 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Planning an efficient upgrade from SQL Server 2005: Step 2 of 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Planning an efficient upgrade from SQL Server 2005: Step 3 of 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   請檢閱[規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)下的需求與考量，包括 [安裝 SQL Server 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   了解如何升級。  
  
    -   檢閱可用的升級方法，並了解[升級資料庫引擎](../../database-engine/install-windows/upgrade-database-engine.md)一文中的規劃與測試方式。  
  
        > [!IMPORTANT]  
        >  您無法將 SQL Server 2005 執行個體就地升級至 SQL Server 2017 伺服器。 您必須安裝 SQL Server 2017 執行個體，然後將 SQL Server 2005 資料庫移轉到新的安裝。 如需詳細資訊，請參閱[選擇資料庫引擎升級方法](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)一文中的＜新安裝升級＞一節。  
   
  
-   如需詳細資訊、指引及取得工具以規劃及自動化您的升級或移轉，請參閱 [不再支援 SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)。  
  
## <a name="get-sql-server"></a>取得 SQL Server  
 若要下載 SQL Server 評估版，請[按一下這裡](http://www.microsoft.com/evalcenter/evaluate-sql-server-2016)。  
  
## <a name="next-steps"></a>Next Steps  
 [SQL Server 2017](http://www.microsoft.com/sql-server/sql-server-2017)   
 [不再支援 SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
  
  
