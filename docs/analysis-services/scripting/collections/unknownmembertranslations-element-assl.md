---
title: "UnknownMemberTranslations 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- UnknownMemberTranslations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- UnknownMemberTranslations
helpviewer_keywords:
- UnknownMemberTranslations element
ms.assetid: 72920843-2d43-4ff4-b38e-19c9a7451cb2
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: be3d45b88c99d7bce92e332154c09461905b1228
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="unknownmembertranslations-element-assl"></a>UnknownMemberTranslations 元素 (ASSL)
  包含標題的翻譯集合[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)維度的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension>  
   ...  
   <UnknownMemberTranslations>  
      <UnknownMemberTranslation xsi:type="Translation ">...</UnknownMemberTranslation>  
      </UnknownMemberTranslations>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|子元素|[UnknownMemberTranslation](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)型別的[轉譯](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**UnknownMemberTranslations**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Translation 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)   
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  