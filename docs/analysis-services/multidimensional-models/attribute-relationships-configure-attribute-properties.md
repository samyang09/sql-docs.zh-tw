---
title: "設定屬性關聯性屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- flexible relationships (Analysis Services)
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
- properties [Analysis Services], attribute relationships
- rigid relationships (Analysis Services)
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bcc42c8bcd73c52851f3ed7fae5f4f7a4915b450
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="attribute-relationships---configure-attribute-properties"></a>屬性關聯性-設定屬性的屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
下表列出及描述屬性 (Attribute) 關聯性的屬性 (Property)。  
  
|屬性|說明|  
|--------------|-----------------|  
|Attribute|包含屬性的名稱。|  
|基數|指出關聯性的基數。 值可為許多 (針對多對一的關聯性)，或是一 (針對一對一的關聯性)。 預設值是「許多」。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，Cardinality 屬性沒有作用，它是保留以備將來實作使用。|  
|名稱|包含屬性的易記名稱。|  
|RelationshipType|指出成員關聯性是否會隨時間變更。 值可為 Rigid，表示成員之間的關聯性並不會隨著時間變更；或為 Flexible，表示成員之間的關聯性會隨時間變更。 預設值是 Flexible。 如果將關聯性定義為彈性，彙總會進行卸除，並重新計算做為累加式更新的一部分 (如果只是加入新成員，就不會卸除)。 如果將關聯性定義為固定，當維度進行累加式更新時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會保留彙總。 如果定義為固定的關聯性變更了， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會在累加式處理期間產生錯誤。 指定適當的關聯性和關聯性屬性可增加查詢和處理效能。|  
|Visible|決定屬性關聯性是否可見。 值為 True 或 False。 預設值是 True。|  
  
  
