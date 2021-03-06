---
title: sys.dm_sql_referenced_entities (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 11/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_sql_referenced_entities_TSQL
- dm_sql_referenced_entities
- sys.dm_sql_referenced_entities
- sys.dm_sql_referenced_entities_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referenced_entities dynamic management function
ms.assetid: 077111cb-b860-4d61-916f-bac5d532912f
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a1ca935166f5d7f955594aafc2e8ff96ee566d8d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmsqlreferencedentities-transact-sql"></a>sys.dm_sql_referenced_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指定之參考實體的定義中依據名稱參考的每個使用者定義實體，各傳回一個資料列。 一個使用者定義的實體呼叫時，會建立兩個實體之間的相依性*受參考實體*，會出現在另一個使用者定義的實體，稱為的保存 SQL 運算式中依名稱*參考實體*. 例如，如果某個預存程序為指定的參考實體，這個函數就會傳回在預存程序中參考的所有使用者定義實體，例如資料表、檢視表、使用者定義型別 (UDT) 或其他預存程序。  
  
 您可以使用這個動態管理函數來回報下列由指定之參考實體所參考的實體類型：  
  
-   結構描述繫結的實體  
  
-   非結構描述繫結的實體  
  
-   跨資料庫與跨伺服器的實體  
  
-   結構描述繫結和非結構描繫結實體的資料行層級相依性  
  
-   使用者定義型別 (別名和 CLR UDT)  
  
-   XML 結構描述集合  
  
-   資料分割函數  
  
**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
sys.dm_sql_referenced_entities (  
    ' [ schema_name. ] referencing_entity_name ' , ' <referencing_class> ' )  
  
<referencing_class> ::=  
{  
    OBJECT  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
```  
  
## <a name="arguments"></a>引數  
 [ *schema_name*。 ] *referencing_entity_name*  
 這是參考實體的名稱。 *schema_name*參考類別為 OBJECT 時，就需要。  
  
 *schema_name.referencing_entity_name*是**nvarchar （517)**。  
  
 *< Referencing_class >* :: = {物件 |DATABASE_DDL_TRIGGER |SERVER_DDL_TRIGGER}  
 這是指定之參考實體的類別。 每個陳述式只能指定一個類別。  
  
 *< referencing_class >*是**nvarchar （60)**。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|referencing_minor_id|**int**|當參考實體是資料行時，就是資料行識別碼，否則便是 0。 不可為 Null。|  
|referenced_server_name|**sysname**|受參考實體之伺服器的名稱。<br /><br /> 這個資料行會因透過指定有效的四部分名稱所達成的跨伺服器相依性而擴展。 多部分名稱的相關資訊，請參閱[TRANSACT-SQL 語法慣例&#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。<br /><br /> 若為參考了實體的非結構描述繫結相依性，但沒有指定四部分名稱，則為 NULL。<br /><br /> 結構描述繫結的實體為 NULL; 因為它們必須位於相同的資料庫，因此只能定義使用兩部分 (*schema.object*) 名稱。|  
|referenced_database_name|**sysname**|受參考實體之資料庫的名稱。<br /><br /> 這個資料行會因透過指定有效的三部分或四部分名稱所達成的跨資料庫或跨伺服器參考而擴展。<br /><br /> 在使用一部分或兩部分名稱指定時，若為非結構描述繫結參考，則為 NULL。<br /><br /> 結構描述繫結的實體為 NULL; 因為它們必須位於相同的資料庫，因此只能定義使用兩部分 (*schema.object*) 名稱。|  
|referenced_schema_name|**sysname**|受參考實體所屬的結構描述。<br /><br /> 若為參考了實體的非結構描述繫結參考，但沒有指定結構描述名稱，則為 NULL。<br /><br /> 若為結構描述繫結的參考，則永遠不會是 NULL。|  
|referenced_entity_name|**sysname**|受參考實體的名稱。 不可為 Null。|  
|referenced_minor_name|**sysname**|當受參考實體是資料行時，就是資料行名稱，否則便是 NULL。 例如，在列出受參考實體本身的資料列中，referenced_minor_name 是 NULL。<br /><br /> 當資料行在參考實體中由名稱所識別，或者父實體用於 SELECT * 陳述式時，受參考的實體就是資料行。|  
|referenced_id|**int**|受參考實體的識別碼。 當 referenced_minor_id 不是 0 時，referenced_id 就是在其中定義資料行的實體。<br /><br /> 若為跨伺服器參考，則一律是 NULL。<br /><br /> 因為資料庫離線或者找不到實體，無法判斷識別碼時，若為跨資料庫參考，則為 NULL。<br /><br /> 無法判斷識別碼時，若為資料庫中的參考，則為 NULL。 非結構描述繫結參考的識別碼時，無法解析參考的實體不存在資料庫中，或名稱解析是呼叫端相依。  在後者的情況下，is_caller_dependent 會設定為 1。<br /><br /> 若為結構描述繫結的參考，則永遠不會是 NULL。|  
|referenced_minor_id|**int**|當受參考實體是資料行時，就是資料行識別碼，否則便是 0。 例如，在列出受參考實體本身的資料列中，referenced_minor_is 是 0。<br /><br /> 若為非結構描述繫結參考，則只有在所有受參考的實體都可以繫結時，才會報告資料行相依性。 如果無法繫結任何受參考的實體，就不會報告任何資料行層級相依性，而且 referenced_minor_id 就是 0。 請參閱範例 D。|  
|referenced_class|**tinyint**|受參考實體的類別。<br /><br /> 1 = 物件或資料行<br /><br /> 6 = 類型<br /><br /> 10 = XML 結構描述集合<br /><br /> 21 = 資料分割函數|  
|referenced_class_desc|**nvarchar(60)**|受參考實體之類別的描述。<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION|  
|is_caller_dependent|**bit**|指出在執行階段發生之受參考實體的結構描述繫結。因此，實體識別碼的解析會相依於呼叫端的結構描述。 當受參考的實體為預存程序、擴充預存程序，或在 EXECUTE 陳述式內部呼叫的使用者定義函數時，就會發生這個事件。<br /><br /> 1 = 受參考的實體是呼叫端相依，而且在執行階段解析。 在此情況下，referenced_id 是 NULL。<br /><br /> 0 = 受參考的實體識別碼不是呼叫端相依。 若為結構描述繫結參考，以及明確指定結構描述名稱的跨資料庫和跨伺服器參考，則一律是 0。 例如，採用 `EXEC MyDatabase.MySchema.MyProc` 格式的實體參考與呼叫端無關。 不過，採用 `EXEC MyDatabase..MyProc` 格式的參考即與呼叫端相關。|  
|is_ambiguous|**bit**|指出參考模稜兩可，而且可以在執行階段解析成的使用者定義函數、 使用者定義型別 (UDT) 或類型的資料行的 xquery 參考**xml**。 例如，假設 `SELECT Sales.GetOrder() FROM Sales.MySales` 陳述式是在預存程序中定義。 在執行該預存程序之前，不知道 `Sales.GetOrder()` 是 `Sales` 結構描述中的使用者自訂函數，還是名為 `Sales`、類型是 UDT 而且具有名為 `GetOrder()` 之方法的資料行。<br /><br /> 1 = 使用者定義函數或資料行與使用者定義型別 (UDT) 方法的參考模糊不清。<br /><br /> 0 = 參考不會模糊不清，或者在呼叫函數時，可成功繫結實體。<br /><br /> 若為結構描述繫結的參考，一律是 0。|  
|is_selected|**bit**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 選取物件或資料行。|  
|is_updated|**bit**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 修改物件或資料行。|  
|is_select_all|**bit**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 在 SELECT * 子句中使用此物件 (只限物件層級)。|  
|is_all_columns_found|**bit**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 可以找到物件的所有資料行相依性。<br /><br /> 0 = 無法找到物件的資料行相依性。|
|is_insert_all|**bit**|**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 物件用於 INSERT 陳述式沒有資料行清單 （只限物件層級）。|  
|is_incomplete|**bit**|**適用於**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 至[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 物件或資料行繫結錯誤，且不完整。|
  
## <a name="exceptions"></a>例外狀況  
 在下列任何情況下，都會傳回空的結果集：  
  
-   已指定系統物件。  
  
-   指定的實體不存在目前的資料庫中。  
  
-   指定的實體沒有參考任何實體。  
  
-   傳遞了無效的參數。  
  
 當指定的參考實體是已編號的預存程序時，就會傳回錯誤。  
  
 無法解析資料行相依性時，就會傳回錯誤 2020。 這個錯誤不會讓查詢無法傳回物件層級相依性。  
  
## <a name="remarks"></a>備註  
 這個函數可以在任何資料庫的內容中執行，以便傳回參考伺服器層級 DDL 觸發程序的實體。  
  
 下表將列出建立並維護相依性資訊的實體類型。 系統不會針對規則、預設值、暫存資料表、暫存預存程序或系統物件建立或維護相依性資訊。  
  
|實體類型|參考實體|受參考的實體|  
|-----------------|------------------------|-----------------------|  
|Table|是*|是|  
|檢視|是|是|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序**|是|是|  
|CLR 預存程序|否|是|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 使用者定義函數|是|是|  
|CLR 使用者定義函數|否|是|  
|CLR 觸發程序 (DML 和 DDL)|否|否|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DML 觸發程序|是|否|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 資料庫層級 DDL 觸發程序|是|否|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器層級 DDL 觸發程序|是|否|  
|擴充預存程序|否|是|  
|佇列|否|是|  
|同義字|否|是|  
|類型 (別名和 CLR 使用者定義型別)|否|是|  
|XML 結構描述集合|否|是|  
|分割區函數|否|是|  
  
 \* 資料表參考時，才會追蹤當做參考實體[!INCLUDE[tsql](../../includes/tsql-md.md)]模組、 使用者定義型別或定義中的計算資料行、 CHECK 條件約束或 DEFAULT 條件約束的 XML 結構描述集合。  
  
 ** 所包含之整數值大於 1 的編號預存程序不會當做參考或受參考的實體進行追蹤。  
  
## <a name="permissions"></a>Permissions  
 需要 sys.dm_sql_referenced_entities 的 SELECT 權限和參考實體的 VIEW DEFINITION 權限。 根據預設，SELECT 權限會授與 public。 當參考實體為資料庫層級 DDL 觸發程序時，便需要資料庫的 VIEW DEFINITION 權限，或資料庫的 ALTER DATABASE DDL TRIGGER 權限。 當參考實體為伺服器層級 DDL 觸發程序時，便需要伺服器的 VIEW ANY DEFINITION 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-entities-that-are-referenced-by-a-database-level-ddl-trigger"></a>A. 傳回資料庫層級 DDL 觸發程序所參考的實體  
 下列範例會傳回資料庫層級 DDL 觸發程序 `ddlDatabaseTriggerLog` 所參考的實體 (資料表和資料行)：  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referenced_schema_name, referenced_entity_name, referenced_minor_name,   
    referenced_minor_id, referenced_class_desc  
FROM sys.dm_sql_referenced_entities ('ddlDatabaseTriggerLog', 'DATABASE_DDL_TRIGGER');  
GO  
```  
  
### <a name="b-returning-entities-that-are-referenced-by-an-object"></a>B. 傳回物件所參考的實體  
 下列範例會傳回使用者定義函數 `dbo.ufnGetContactInformation` 所參考的實體。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referenced_schema_name, referenced_entity_name, referenced_minor_name,   
    referenced_minor_id, referenced_class_desc, is_caller_dependent, is_ambiguous  
FROM sys.dm_sql_referenced_entities ('dbo.ufnGetContactInformation', 'OBJECT');  
GO  
```  
  
### <a name="c-returning-column-dependencies"></a>C. 傳回資料行相依性  
 下列範例會以計算資料行 `Table1` 定義為資料行 `c` 和 `a` 的總和，建立資料表 `b`。 然後系統會呼叫 `sys.dm_sql_referenced_entities` 檢視表。 接著，此檢視表會傳回兩個資料列 (針對計算資料行中定義的每個資料行各傳回一個資料列)。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.Table1 (a int, b int, c AS a + b);  
GO  
SELECT referenced_schema_name AS schema_name,  
    referenced_entity_name AS table_name,  
    referenced_minor_name AS referenced_column,  
    COALESCE(COL_NAME(OBJECT_ID(N'dbo.Table1'),referencing_minor_id), 'N/A') AS referencing_column_name  
FROM sys.dm_sql_referenced_entities ('dbo.Table1', 'OBJECT');  
GO

-- Remove the table.  
DROP TABLE dbo.Table1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 schema_name table_name referenced_column referencing_column  
 ----------- ---------- ----------------- ------------------  
 dbo         Table1     a                 c  
 dbo         Table1     b                 c  
```

### <a name="d-returning-non-schema-bound-column-dependencies"></a>D. 傳回非結構描述繫結的資料行相依性  
 下列範例會卸除 `Table1` 並建立 `Table2` 和預存程序 `Proc1`。 此程序會參考 `Table2` 和不存在的資料表 `Table1`。 然後，系統會執行檢視表 `sys.dm_sql_referenced_entities`，並將預存程序指定成參考實體。 結果集會針對 `Table1` 顯示一個資料列，並針對 `Table2` 顯示 3 個資料列。 因為 `Table1` 不存在，所以無法解析資料行相依性，而且會傳回錯誤 2020。 `is_all_columns_found` 資料行會針對 `Table1` 傳回 0，表示有資料行找不到。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.Table1', 'U' ) IS NOT NULL   
    DROP TABLE dbo.Table1;  
GO  
CREATE TABLE dbo.Table2 (c1 int, c2 int);  
GO  
CREATE PROCEDURE dbo.Proc1 AS  
    SELECT a, b, c FROM Table1;  
    SELECT c1, c2 FROM Table2;  
GO  
SELECT referenced_id, referenced_entity_name AS table_name, referenced_minor_name AS referenced_column_name, is_all_columns_found  
FROM sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1  
 935674381     Table2       C1                      1  
 935674381     Table2       C2                      1  
 NULL          Table1       NULL                    0  

 Msg 2020, Level 16, State 1, Line 1The dependencies reported for entity "dbo.Proc1" might not include references to all columns. This is either because the entity references an object that does not exist or because of an error in one or more statements in the entity.  Before rerunning the query, ensure that there are no errors in the entity and that all objects referenced by the entity exist.
 ```
  
### <a name="e-demonstrating-dynamic-dependency-maintenance"></a>E. 示範動態相依性維護  
 下列範例會擴充範例 D，以便展示如何以動態方式維護相依性。 此範例首先會重新建立 `Table1` (之前在範例 D 中卸除)。然後，系統會再次執行 `sys.dm_sql_referenced_entities`，並將預存程序指定成參考實體。 結果集顯示，資料表以及其在預存程序中定義的各自資料行都會傳回。 此外，`is_all_columns_found` 資料行會針對所有物件和資料行傳回 1。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (a int, b int, c AS a + b);  
GO   
SELECT referenced_id, referenced_entity_name AS table_name, referenced_minor_name as column_name, is_all_columns_found  
FROM sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');  
GO  
DROP TABLE Table1, Table2;  
DROP PROC Proc1;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1 
 935674381     Table2       c1                      1 
 935674381     Table2       c2                      1 
 967674495     Table1       NULL                    1 
 967674495     Table1       a                       1  
 967674495     Table1       b                       1  
 967674495     Table1       c                       1  
 ```
 
### <a name="f-returning-object-or-column-usage"></a>F. 傳回物件或資料行使用方式  
 下列範例會傳回 `HumanResources.uspUpdateEmployeePersonalInfo` 預存程序的物件和資料行相依性。 此程序更新資料行`NationalIDNumber`， `BirthDate,``MaritalStatus`，和`Gender`的`Employee`資料表根據指定`BusinessEntityID`值。 在 TRY…CATCH 區塊中定義另一個預存程序 `upsLogError`，以擷取任何執行錯誤。 `is_selected`、`is_updated` 和 `is_select_all` 資料行會傳回如何在參考物件中使用這些物件和資料行的相關資訊。 修改的資料表和資料行會在 is_updated 資料行中由 1 表示。 只選取 `BusinessEntityID` 資料行，而且不會選取或修改 `uspLogError` 預存程序。  
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql  
SELECT referenced_entity_name AS table_name, referenced_minor_name as column_name, is_selected, is_updated, is_select_all  
FROM sys.dm_sql_referenced_entities ('HumanResources.uspUpdateEmployeePersonalInfo', 'OBJECT');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 table_name    column_name         is_selected is_updated is_select_all  
 ------------- ------------------- ----------- ---------- -------------  
 uspLogError   NULL                0           0          0  
 Employee      NULL                0           1          0  
 Employee      BusinessEntityID    1           0          0  
 Employee      NationalIDNumber    0           1          0  
 Employee      BirthDate           0           1          0  
 Employee      MaritalStatus       0           1          0  
 Employee      Gender              0           1          0
 ```
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
