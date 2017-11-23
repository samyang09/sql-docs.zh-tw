---
title: "sys.asymmetric_keys (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- asymmetric_keys
- sys.asymmetric_keys_TSQL
- asymmetric_keys_TSQL
- sys.asymmetric_keys
dev_langs: TSQL
helpviewer_keywords: sys.asymmetric_keys catalog view
ms.assetid: bbca796a-9bb5-4a62-9ca8-1d255984553d
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c42b7a6bcc17fff443fbbafd960baba6bc359ef
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysasymmetrickeys-transact-sql"></a>sys.asymmetric_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對每一個非對稱金鑰，各傳回一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|金鑰的名稱。 在資料庫中，這是唯一的。|  
|**principal_id**|**int**|擁有金鑰的資料庫主體識別碼。|  
|**asymmetric_key_id**|**int**|金鑰的識別碼。 在資料庫中，這是唯一的。|  
|**pvt_key_encryption_type**|**char(2)**|金鑰的加密方式。<br /><br /> NA = 未加密<br /><br /> MK = 金鑰由主要金鑰加密<br /><br /> PW = 金鑰由使用者自訂密碼加密<br /><br /> SK = 金鑰由服務主要金鑰加密。|  
|**pvt_key_encryption_type_desc**|**nvarchar （60)**|私密金鑰加密方式的描述。<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**憑證指紋**|**varbinary(32)**|金鑰的 SHA-1 雜湊。 此雜湊是全域唯一的。|  
|**演算法**|**char(2)**|金鑰使用的演算法。<br /><br /> 1R = 512 位元 RSA<br /><br /> 2R = 1024 位元 RSA<br /><br /> 3R = 2048 位元 RSA|  
|**algorithm_desc**|**nvarchar （60)**|金鑰使用之演算法的描述。<br /><br /> RSA_512<br /><br /> RSA_1024<br /><br /> RSA_2048|  
|**key_length**|**int**|金鑰的位元長度。|  
|**sid**|**varbinary(85)**|這個金鑰的登入 SID。 如果是 Extensible Key Management 金鑰，這個值將會是 NULL。|  
|**string_sid**|**nvarchar （128)**|金鑰的登入 SID 字串表示法。 如果是 Extensible Key Management 金鑰，這個值將會是 NULL。|  
|**public_key**|**varbinary(max)**|公開金鑰。|  
|**attested_by**|**nvarchar （260)**|僅供系統使用。|  
|**provider_type**|**nvarchar(120)**|密碼編譯提供者的類型：<br /><br /> CRYPTOGRAPHIC PROVIDER = Extensible Key Management 金鑰<br /><br /> NULL = 非 Extensible Key Management 金鑰|  
|**cryptographic_provider_guid**|**uniqueidentifier**|密碼編譯提供者的 GUID。 如果是非 Extensible Key Management 金鑰，這個值將會是 NULL。|  
|**cryptographic_provider_algid**|**sql_variant**|密碼編譯提供者的演算法識別碼。 如果是非 Extensible Key Management 金鑰，這個值將會是 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
  