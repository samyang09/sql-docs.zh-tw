---
title: "狀態屬性 (ADO MD) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1886dae43bdb764a67fa5e44b1e8fe9744c0cb5f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="state-property-ado-md"></a>State 屬性 (ADO MD)
表示資料格集的目前狀態。  
  
## <a name="return-values"></a>傳回值  
 傳回**長**整數，指出目前的狀況[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件，並為唯讀。 下列是有效值： **adStateClosed** (0) 和**adStateOpen** (1)。  
  
## <a name="remarks"></a>備註  
 若要使用[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)常數的名稱，您必須在專案中參考的 ADO 類型程式庫。 請參閱[使用 ADO 與 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)如需詳細資訊。  
  
## <a name="applies-to"></a>適用於  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Close 方法 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
