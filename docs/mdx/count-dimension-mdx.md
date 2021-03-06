---
title: Count （維度） (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- Count function [MDX]
ms.assetid: 4b9c52f6-5bb0-401a-947c-e14134558b4a
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7c75e556f86ad2c433e97e44474048e042603861
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="count-dimension-mdx"></a>Count (維度) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回 Cube 中的階層數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>備註  
 傳回 Cube 中的階層數目，包括 `[Measures].[Measures]` 階層。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Adventure Works Cube 中的階層數目。  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱  
 [計數 &#40;Tuple &#41;&#40;MDX &#41;](../mdx/count-tuple-mdx.md)   
 [計數 &#40;階層層級 &#41;&#40;MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [計數 &#40;設定 &#41;&#40;MDX &#41;](../mdx/count-set-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
