---
title: SET OFFSETS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_OFFSETS_TSQL
- OFFSETS_TSQL
- SET OFFSETS
- OFFSETS
dev_langs:
- TSQL
helpviewer_keywords:
- position relative to start of statement [SQL Server]
- OFFSETS option
- offsets [SQL Server]
- SET OFFSETS statement
ms.assetid: c7bcc697-0930-4630-acae-d8ccbfa4414c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 232550be5756505082b615a84ccbd35ef84b1477
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="set-offsets-transact-sql"></a>SET OFFSETS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中之指定關鍵字的位移 (相對於陳述式起點的位置) 傳回 DB-Library 應用程式。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET OFFSETS keyword_list { ON | OFF }  
```  
  
## <a name="arguments"></a>引數  
 *keyword_list*  
 這是一份 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建構清單 (以逗號分隔)，其中包括 SELECT、FROM、ORDER、TABLE、PROCEDURE、STATEMENT、PARAM 和 EXECUTE。  
  
## <a name="remarks"></a>Remarks  
 只有在 DB-Library 應用程式中，才會使用 SET OFFSETS。  
  
 SET OFFSETS 的設定是在剖析階段進行設定，而不是在執行階段進行設定。 在剖析階段進行設定意謂著，如果 SET 陳述式在批次或預存程序中，不論程式碼是否實際執行到這一點，設定都會生效；SET 陳述式會在執行任何陳述式之前生效。 例如，即使 SET 陳述式是在永遠不會執行到的 IF...ELSE 陳述式區塊中，SET 陳述式仍會生效，因為會剖析 IF...ELSE 陳述式區塊。  
  
 如果 SET OFFSETS 設在預存程序中，從預存程序傳回控制權之後，會還原 SET OFFSETS 的值。 因此，動態 SQL 中所指定的 SET OFFSETS 陳述式完全不會影響在動態 SQL 陳述式之後的任何陳述式。  
  
 如果 OFFSETS 選項是 ON，或未發生任何錯誤，SET PARSEONLY 會傳回位移。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET PARSEONLY &#40;Transact-SQL&#41;](../../t-sql/statements/set-parseonly-transact-sql.md)  
  
  
