---
title: "SQL Server on Linux 的客戶意見反應 |Microsoft 文件"
description: "描述如何收集並在 Linux 上設定 SQL Server 客戶回函。"
author: annashres
ms.author: anshrest
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 25772bd0ad7b2994e732e97fd264bef0e951eea9
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="customer-feedback-for-sql-server-on-linux"></a>SQL Server on Linux 的客戶意見反應

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

根據預設，Microsoft SQL Server 會收集客戶如何使用應用程式的相關資訊。 具體來說，SQL Server 會收集有關安裝體驗、使用情況和效能的相關資訊。 這些資訊可協助 Microsoft 改善產品，以進一步滿足客戶需求。 例如，Microsoft 會收集客戶所遇到之錯誤代碼的相關資訊，以便修正相關錯誤、改善如何使用 SQL Server 的相關文件，以及判斷是否應將功能加入到產品中以滿足客戶。

本文件提供詳細資料會收集哪些類型的資訊以及有關如何設定 Microsoft SQL Server 上傳送，收集的 Linux 資料給 Microsoft 的資訊。 SQL Server 2017 包含隱私權聲明，說明我們並不會從使用者收集哪些資訊。 請閱讀隱私權聲明。

具體來說，Microsoft 不會透過此機制傳送下列類型的資訊：

- 使用者資料表內的任何值
- 任何登入認證或其他驗證資訊
- 個人識別資訊 (PII)

SQL Server 2017 一律會收集並傳送與安裝程序中安裝體驗相關的資訊，以便我們能夠快速找出並修正客戶所遇到的任何安裝問題。 SQL Server 2017 可以設定成不 （針對每個伺服器執行個體） 的資訊傳送到透過 Microsoft **mssql conf**。 mssql conf 是隨 SQL Server 2017 Red Hat Enterprise Linux、 SUSE Linux Enterprise Server 和 Ubuntu 組態指令碼。

> [!NOTE]
> 您僅可在付費版本的 SQL Server 中停用將資訊傳送給 Microsoft 的功能。

## <a name="disable-customer-feedback"></a>停用客戶的意見反應

此選項可讓您如果 SQL Server 會傳送給 Microsoft 的意見反應或未變更。 依預設，此值設定為 true。 若要變更的值，執行下列命令：

### <a name="on-red-hat-suse-and-ubuntu"></a>Red Hat、 SUSE，和 Ubuntu

1. 以具有 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.customerfeedback**。 下列範例藉由指定關閉客戶的意見反應**false**。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker
若要停用 docker 的客戶的意見反應，您必須擁有 Docker[保存您的資料](sql-server-linux-configure-docker.md)。 

1. 新增`mssql.conf`檔案行`[telemetry]`和`customerfeedback = false`主機目錄中：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```
2. 執行容器映像
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="local-audit-for-sql-server-on-linux-usage-feedback-collection"></a>本機 for SQL Server on Linux 使用量意見反應收集的稽核

Microsoft SQL Server 2017 包含網際網路通訊功能，收集，並將您的電腦或裝置 （「 標準電腦資訊 」） 的相關資訊傳送給 Microsoft。 SQL Server 使用意見集合的本機稽核元件可以撰寫資料服務所收集到指定的資料夾，表示將會傳送給 Microsoft 的資料 （記錄）。 本機稽核的目的是要讓客戶看到 Microsoft 以此功能收集的所有資料，以用於相容性、法規或隱私權驗證的理由。

在 Linux 上的 SQL Server，本機稽核是可以設定在 SQL Server Database Engine 的執行個體層級。 其他 SQL Server 元件和 SQL Server 工具不會擁有使用量意見反應收集本機稽核功能。

### <a name="enable-local-audit"></a>啟用本機稽核

此選項可讓本機稽核，並可讓您設定目錄建立本機的稽核記錄檔的位置。

1. 建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新**/tmp/稽核**目錄：

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. 以具有 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker
若要啟用本機稽核 docker，您必須擁有 Docker[保存您的資料](sql-server-linux-configure-docker.md)。 

1. 新的本機稽核記錄檔的目標目錄會在容器中。 在您的電腦上的主機目錄建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新**/稽核**目錄：

   ```bash
   sudo mkdir <host directory>/audit
   ```

   
1. 新增`mssql.conf`檔案行`[telemetry]`和`userrequestedlocalauditdirectory = <host directory>/audit`主機目錄中：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```
2. 執行容器映像
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="next-steps"></a>後續的步驟

如需有關 SQL Server on Linux，請參閱[概觀的 SQL Server on Linux](sql-server-linux-overview.md)。
