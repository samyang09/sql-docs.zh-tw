---
title: "-= (減法指派) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- -=
- -=_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, -=
- assignment operators, -=
- augmented operators, -=
- -= (subtract equals)
- -= (subtraction assignment)
ms.assetid: 2a2056b5-1dfa-4ea8-8cfc-6331a2f94da9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e42283367d3035ce4d7fcaecb4f7c96bcb7fed68
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="--subtraction-assignment-transact-sql"></a>-= (減法指派) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  兩數相減，再將值設定為運算結果。 例如，如果變數 @x 等於 35，則 @x -= 2 會用 @x 的原始值減去 2，然後將 @x 設定為該新值 (33)。  
  
## <a name="syntax"></a>語法  
  
```  
expression -= expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 這是數值類別目錄中任何一個資料類型的任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，但是 **bit** 資料類型除外。  
  
## <a name="result-types"></a>結果類型  
 傳回優先順序較高之引數的資料類型。 如需詳細資訊，請參閱[資料類型優先順序 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 如需詳細資訊，請參閱 [- &#40;減法&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/subtract-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [複合運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
