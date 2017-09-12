---
title: "@@SERVICENAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SERVICENAME_TSQL'
- '@@SERVICENAME'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVICENAME function'
- names [SQL Server], registry keys
- registry keys [SQL Server]
ms.assetid: 5b0b35be-50ae-411d-a607-bf7464b73624
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8e93602aed47f8b5147d39eaf41503488f57a855
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="servicename-transact-sql"></a>@@SERVICENAME (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回用來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的登錄機碼名稱。 @@SERVICENAME傳回 'MSSQLSERVER'，如果目前的執行個體是預設執行個體; 如果目前的執行個體是具名執行個體，此函數會傳回執行個體名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
@@SERVICENAME  
```  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar**  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行為 MSSQLServer 服務。  
  
## <a name="examples"></a>範例  
 下列範例會顯示如何使用 `@@SERVICENAME`。  
  
```  
SELECT @@SERVICENAME AS 'Service Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Service Name                    
------------------------------  
MSSQLSERVER                     
```  
  
## <a name="see-also"></a>另請參閱  
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [管理 Database Engine Services](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  