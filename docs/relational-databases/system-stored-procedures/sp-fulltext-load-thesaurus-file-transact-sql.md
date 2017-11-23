---
title: "sp_fulltext_load_thesaurus_file (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fulltext_load_thesaurus_file
- sp_fulltext_load_thesaurus_file_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_fulltext_load_thesaurus_file
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], editing
ms.assetid: 73a309c3-6d22-42dc-a6fe-8a63747aa2e4
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b50288eae8d0deb0f0a91dc64523c579444292c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="spfulltextloadthesaurusfile-transact-sql"></a>sp_fulltext_load_thesaurus_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  造成伺服器執行個體從對應至 LCID 已指定之語言的同義字檔案中剖析並載入資料。 這個預存程序在更新同義字檔案之後很有用。 執行**sp_fulltext_load_thesaurus_file**會導致重新編譯使用指定的 LCID 同義字的全文檢索查詢。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_fulltext_load_thesaurus_file lcid [ , @loadOnlyIfNotLoaded  = action ]   
```  
  
## <a name="arguments"></a>引數  
 *lcid*  
 對應您想要載入同義字 XML 定義之語言地區設定識別碼 (LCID) 的整數。 若要取得之伺服器執行個體可用的語言的 Lcid，請使用[sys.fulltext_languages &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)目錄檢視。  
  
 **@loadOnlyIfNotLoaded** = *動作*  
 指定同義字檔案是否會載入內部同義字資料表中，即使已經載入也是一樣。 *動作*是下列之一：  
  
|值|定義|  
|-----------|----------------|  
|**0**|載入同義字檔案，不管是否已經載入。 這是預設行為的**sp_fulltext_load_thesaurus_file**。|  
|1|只有在尚未載入同義字檔案時，才會載入。|  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 同義字檔案會自動由使用此同義字的全文檢索查詢載入。 若要避免這種第一次效能影響對全文檢索查詢，我們建議您執行**sp_fulltext_load_thesaurus_file**。  
  
 使用[sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**' 來更新使用全文檢索搜尋註冊之語言的清單。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或系統管理員可以執行**sp_fulltext_load_thesaurus_file**預存程序。  
  
 只有系統管理員能夠更新、修改或刪除同義字檔案。  
  
## <a name="examples"></a>範例  
  
### <a name="a-load-a-thesaurus-file-even-if-it-is-already-loaded"></a>A. 載入同義字檔案，即使已經載入也是一樣  
 下列範例會剖析並載入英文同義字檔案。  
  
```  
EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
GO  
```  
  
### <a name="b-load-a-thesaurus-file-only-if-it-is-not-yet-loaded"></a>B. 只有在尚未載入同義字檔案時，才會載入  
 下列範例會剖析並載入阿拉伯文同義字檔案 (除非已經載入)。  
  
```  
EXEC sys.sp_fulltext_load_thesaurus_file 1025, @loadOnlyIfNotLoaded = 1;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [FULLTEXTSERVICEPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
  