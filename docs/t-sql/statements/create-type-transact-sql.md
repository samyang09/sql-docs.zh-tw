---
title: "建立類型 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql13.swb.sysdatatype.properties.f1
- CREATE TYPE
- TYPE_TSQL
- TYPE
- CREATE_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [SQL Server], creating
- CLR user-defined types [SQL Server]
- user-defined table types [SQL Server]
- user-defined types [SQL Server], creating
- CREATE TYPE statement
- alias data types [SQL Server], creating
- data types [SQL Server], creating
ms.assetid: 2202236b-e09f-40a1-bbc7-b8cff7488905
caps.latest.revision: 92
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4e7f411871d98fc6854b97478402567017d28222
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-type-transact-sql"></a>CREATE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 的目前資料庫中建立別名資料類型或使用者定義型別。 別名資料類型的實作是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生系統類型為基礎。 使用者定義型別透過組件中的類別來實作[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]通用語言執行平台 (CLR)。 若要將使用者定義型別繫結到它的實作，包含型別實作的 CLR 組件必須先註冊在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，依預設，執行 CLR 程式碼的功能是關閉。 您可以建立、 修改和卸除參考 managed 程式碼模組的資料庫物件中，將無法執行這些參考，但[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非[clr enabled 選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)啟用利用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
 
> [!NOTE]  
>  在本主題討論.NET Framework CLR 整合 SQL Server。 CLR 整合不適用於 Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Disk-Based Type Syntax  
CREATE TYPE [ schema_name. ] type_name  
{   
    FROM base_type   
    [ ( precision [ , scale ] ) ]  
    [ NULL | NOT NULL ]   
  | EXTERNAL NAME assembly_name [ .class_name ]   
  | AS TABLE ( { <column_definition> | <computed_column_definition> }  
        [ <table_constraint> ] [ ,...n ] )    
} [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   
    [ NULL | NOT NULL ]  
    [   
        DEFAULT constant_expression ]   
      | [ IDENTITY [ ( seed ,increment ) ]   
    ]  
    [ ROWGUIDCOL ] [ <column_constraint> [ ...n ] ]   
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
                [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH ( <index_option> [ ,...n ] )   
        ]  
  | CHECK ( logical_expression )   
}   
  
<computed_column_definition> ::=  
  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH ( <index_option> [ ,...n ] )  
        ]  
    | CHECK ( logical_expression )   
]   
  
<table_constraint> ::=  
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
    ( column [ ASC | DESC ] [ ,...n ] )   
        [   
    WITH ( <index_option> [ ,...n ] )   
        ]  
    | CHECK ( logical_expression )   
}   
  
<index_option> ::=  
{  
    IGNORE_DUP_KEY = { ON | OFF }  
}  
```  
  
```  
-- Memory-Optimized Table Type Syntax  
CREATE TYPE [schema_name. ] type_name  
AS TABLE ( { <column_definition> }  
    |  [ <table_constraint> ] [ ,... n ]    
    | [ <table_index> ] [ ,... n ]    } )
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   [ NULL | NOT NULL ]    [  
      [ IDENTITY [ (1 , 1) ]  
    ]  
    [ <column_constraint> [ ... n ] ]    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
{ PRIMARY KEY {   NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count) 
                | NONCLUSTERED } }  
  
< table_constraint > ::=  
{ PRIMARY KEY { NONCLUSTERED HASH (column [ ,... n ] ) 
                   WITH (BUCKET_COUNT = bucket_count) 
               | NONCLUSTERED  (column [ ASC | DESC ] [ ,... n ] )  } }  
  
<column_index> ::=  
  INDEX index_name  
{ { [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count) 
     | NONCLUSTERED } }  
  
< table_index > ::=  
  INDEX constraint_name  
{ { [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count) 
 |  [NONCLUSTERED]  (column [ ASC | DESC ] [ ,... n ] )} }  
  
<table_option> ::=  
{  
    [MEMORY_OPTIMIZED = {ON | OFF}]  
}  
```  
  
## <a name="arguments"></a>引數  
 *schema_name*  
 這是別名資料類型或使用者自訂類型所屬的結構描述名稱。  
  
 *type_name*  
 這是別名資料類型或使用者自訂類型的名稱。 型別名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 *base_type*  
 是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供的別名資料類型所依據的資料類型。 *base_type*是**sysname**，沒有預設值，它可以是下列值之一：  
  
|||||  
|-|-|-|-|  
|**bigint**|**二進位 (**  *n*  **)**|**bit**|**char (**  *n*  **)**|  
|**date**|**datetime**|**datetime2**|**datetimeoffset**|  
|**decimal**|**float**|**image**|**int**|  
|**money**|**nchar (**  *n*  **)**|**ntext**|**numeric**|  
|**nvarchar (**  *n*  &#124;**最大值)**|**real**|**smalldatetime**|**smallint**|  
|**smallmoney**|**sql_variant**|**text**|**time**|  
|**tinyint**|**uniqueidentifier**|**varbinary (**  *n*  &#124;**最大值)**|**varchar (**  *n*  &#124;**最大值)**|  
  
 *base_type*也可以是對應至這些系統資料類型之一的任何資料類型同義字。  
  
 *有效位數*  
 如**十進位**或**數值**，為非負數的整數，指出可以儲存，左邊和右邊的小數點的十進位數字的最大的總數。 如需詳細資訊，請參閱[decimal 和 numeric &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *scale*  
 如**十進位**或**數值**，是一個非負數整數，指出可儲存小數點右邊的小數位數的數目上限，而且它必須是小於或等於有效位數. 如需詳細資訊，請參閱[decimal 和 numeric &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 **NULL** |不是 NULL  
 指定類型可否保留 Null 值。 若未指定，NULL 是預設值。  
  
 *assembly_name*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]參考 common language runtime 中的使用者定義型別實作的組件。 *assembly_name*應符合中的現有組件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目前資料庫中。  
  
> [!NOTE]  
>  自主資料庫無法使用 EXTERNAL_NAME。  
  
 **[.** *class_name***]**   
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定組件內實作使用者自訂類型的類別。 *class_name*必須是有效的識別項且必須是組件中的類別與組件可見性。 *class_name*區分大小寫，不論資料庫定序，且必須完全符合相對應組件中的類別名稱。 類別名稱可以是以方括弧括住的命名空間限定名稱 (**[]**) 如果用來撰寫類別的程式設計語言使用命名空間，如 C# 的概念。 如果*class_name*未指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假設它是與相同*type_name*。  
  
 \<column_definition >  
 定義使用者定義資料表類型的資料行。  
  
 \<資料類型 >  
 針對使用者定義資料表類型定義資料行中的資料類型。 如需資料類型的詳細資訊，請參閱[資料類型 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/data-types-transact-sql.md). 如需資料表的詳細資訊，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<column_constraint >  
 定義使用者定義資料表類型的資料行條件約束。 支援的條件約束包括 PRIMARY KEY、UNIQUE 和 CHECK。 如需資料表的詳細資訊，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<computed_column_definition >  
 將計算資料行運算式定義為使用者定義資料表類型中的資料行。 如需資料表的詳細資訊，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<table_constraint >  
 定義使用者定義資料表類型上的資料表條件約束。 支援的條件約束包括 PRIMARY KEY、UNIQUE 和 CHECK。  
  
 \<index_option >  
 指定在唯一叢集或唯一非叢集索引的多資料列插入作業中，對於索引鍵值重複的錯誤回應。 如需有關索引選項的詳細資訊，請參閱[CREATE INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 INDEX  
 您必須指定資料行和資料表索引，做為 CREATE TABLE 陳述式的一部分。 記憶體最佳化資料表不支援 CREATE INDEX 和 DROP INDEX。  
  
 MEMORY_OPTIMIZED  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指出資料表類型是否為記憶體最佳化。 此選項預設關閉；資料表 (類型) 不是記憶體最佳化的資料表 (類型)。 記憶體最佳化的資料表類型是記憶體最佳化的使用者資料表，其結構描述保存在磁碟上，類似於其他使用者資料表。  
  
 BUCKET_COUNT  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指出應該在雜湊索引中建立的貯體數目。 雜湊索引中 BUCKET_COUNT 的最大值是 1,073,741,824。 如需有關值區計數的詳細資訊，請參閱[記憶體最佳化資料表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)。 *bucket_count*是必要引數。  
  
 HASH  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 表示已建立雜湊索引。 只有記憶體最佳化的資料表才支援雜湊索引。  
  
## <a name="remarks"></a>備註  
 中所參考的組件類別*assembly_name*，及其方法，必須符合實作使用者定義型別中的所有需求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需有關這些需求的詳細資訊，請參閱[clr 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
 其他考量包括以下各項：  
  
-   類別可以有多載的方法，但只能從 Managed 程式碼內 (不能從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 內) 呼叫這些方法。  
  
-   任何靜態成員必須宣告為**const**或**readonly**如果*assembly_name*是 SAFE 或 EXTERNAL_ACCESS。  
  
 在資料庫內，只能有一個依照已從 CLR 上傳至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中之任何指定類型來註冊的使用者自訂類型。 如果使用者自訂類型建立在某 CLR 類型上，而針對該 CLR 類型，在資料庫中已存在使用者自訂類型，則 CREATE TYPE 會因錯誤而失敗。 如果 CLR 類型可以對應至多個使用者自訂類型，就需要利用這項限制來避免 SQL 類型解析期間的模稜兩可。  
  
 如果型別中的任何 mutator 方法不會傳回*void*，CREATE TYPE 陳述式不會執行。  
  
 若要修改使用者自訂類型，您必須利用 DROP TYPE 陳述式卸除該類型，然後重新建立它。  
  
 不同於使用所建立的使用者定義型別**sp_addtype**、**公用**資料庫角色未自動授與 REFERENCES 權限利用 CREATE TYPE 建立型別。 這個權限必須另外授與。  
  
 在使用者定義資料表類型中，結構化中所使用的使用者定義型別*column_name* \<資料類型 > 的資料表類型定義所在的資料庫結構描述範圍的一部分。 若要在資料庫中存取不同範圍內的結構化使用者定義型別，請使用兩部分的名稱。  
  
 在使用者定義的資料表類型中，計算資料行的主索引鍵必須是 PERSISTED 和 NOT NULL。  
  
## <a name="memory-optimized-table-types"></a>記憶體最佳化的資料表類型  
 從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 開始，資料表類型的資料處理可以在主要記憶體中執行，而不是在磁碟上。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。 如需示範如何建立記憶體最佳化資料表類型程式碼範例，請參閱[建立記憶體最佳化資料表和原生編譯預存程序](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)。  
  
## <a name="permissions"></a>Permissions  
 需要目前資料庫的 CREATE TYPE 權限，以及 *schema_name*的 ALTER 權限。 如果未指定 *schema_name* ，則套用用來判斷目前使用者之結構描述的預設名稱解析規則。 如果*assembly_name*會指定，使用者必須擁有組件或對它的 REFERENCES 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-an-alias-type-based-on-the-varchar-data-type"></a>A. 根據 varchar 資料類型建立別名類型  
 下列範例根據系統提供的 `varchar` 資料類型建立別名資料類型。  
  
```  
CREATE TYPE SSN  
FROM varchar(11) NOT NULL ;  
```  
  
### <a name="b-creating-a-user-defined-type"></a>B. 建立使用者自訂類型  
 下列範例會建立型別`Utf8String`參考類別`utf8string`組件中`utf8string`。 建立該類型之前，必須先在本機資料庫中註冊 `utf8string` 組件。 以有效的描述取代 CREATE ASSEMBLY 陳述式的二進位部分。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE ASSEMBLY utf8string  
AUTHORIZATION [dbi]   
FROM 0x4D... ;  
GO  
CREATE TYPE Utf8String   
EXTERNAL NAME utf8string.[Microsoft.Samples.SqlServer.utf8string] ;  
GO  
```  
  
### <a name="c-creating-a-user-defined-table-type"></a>C. 建立使用者自訂資料表類型  
 下列範例會建立有兩個資料行的使用者定義資料表類型。 如需如何建立及使用資料表值參數的詳細資訊，請參閱[使用資料表值參數 &#40; Database engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
```  
CREATE TYPE LocationTableType AS TABLE   
    ( LocationName VARCHAR(50)  
    , CostRate INT );  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立組件 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [卸除類型 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
