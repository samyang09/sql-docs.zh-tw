---
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d59963510a71f552602577fce196e014cafe907
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="localdberrorinstanceexistswithlowerversion"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|258|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|無法以指定的版本建立本機資料庫執行個體。 已存在相同名稱之執行個體，但其版本較指定的版本舊。|  
  
## <a name="explanation"></a>說明  
 指定的執行個體已經存在，但是其版本低於要求的版本。  
  
## <a name="user-action"></a>使用者動作  
 請刪除現有的執行個體，然後再重試作業。  
  
  
