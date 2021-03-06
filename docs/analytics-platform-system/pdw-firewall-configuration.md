---
title: PDW 防火牆設定 (Analytics Platform System)
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
ms.assetid: 191f292d-16bc-4166-b855-158854ad062d
caps.latest.revision: 28
ms.openlocfilehash: 8795f2254160a4ba605643b89dc4b9df0cce4c7f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="pdw-firewall-configuration"></a>PDW 防火牆設定
**防火牆**頁面的 SQL Server PDW 組態管理員可讓您啟用或停用防火牆規則來允許或防止 Analytics Platform System 應用裝置上的特定連接埠存取。  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>若要管理的連接埠和防火牆應用裝置節點的規則  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱[啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在左窗格中的 Configuration Manager 中，依序展開**平行資料倉儲拓樸**，然後按一下 **防火牆**。  
  
3.  找出連接埠或防火牆規則，若要更新的組態清單中，然後選取或清除項目旁的方塊。 SQL Server PDW 系統管理員可設定選項會顯示在此清單中，包括開頭和結尾對外公開的節點上的連接埠。  
  
4.  按一下**套用**以儲存變更。  
  
![DWConfig 應用裝置 PDW 防火牆](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>外部連接埠  
下列的連接埠已開啟用於來自 PDW 之外的用戶端連線。  
  
|目的|連接埠 #|節點|  
|-----------|-----------|---------|  
|SQL 用戶端存取 PDW (TDS)|17001|CTL|  
|載入器用戶端存取 (dwloader & S)|8001|CTL|  
|遠端桌面存取|3389|CMP 的 CTL|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL 加密連線 （適用於內部通訊，來存取管理主控台，並存取 HDInsight 叢集服務）|443|所有節點|  
|SQL Server PDW 負載控制流程的 Windows 認證|8002|CTL|  
|_Kerberos|88|AD01 和 ad02 移，|  
|_ldap|389|AD01 和 ad02 移|  
  
## <a name="internal-ports"></a>內部連接埠  
下列連接埠的 PDW 用於內部通訊，但來自外部 PDW 應用裝置的連接未開啟。  
  
|目的|連接埠 #|節點|  
|-----------|-----------|---------|  
|DMS 控制通道流量|16450|CMP 的 CTL|  
|DMS 資料通道流量|16550|CMP 的 CTL|  
|內部診斷|16650|CMP 的 CTL|  
|容錯移轉狀態 (DMS)|15000|CMP 的 CTL|  
|容錯移轉狀態 (Engine)|15001|CMP|  
|動態 （暫時） 連接埠範圍|20000-65535|CMP 的 CTL|  
|SQL Server 連接埠範圍 (TDS)|1433, 1500-1508|CMP 的 CTL|  
  
> [!NOTE]  
> 建立外部資料表或外部資料來源會使用預設的 TCP 連接埠 8020。 這些陳述式可以設定改為使用其他連接埠。 50300 Hortonworks JOB_TRACKER_LOCATION 預設連接埠。 與其他系統和工具整合，可能需要額外的連接埠。  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
