---
title: Dbms 中的交易支援 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4dea29ad82564aa30bdc0c4dbacd3e560ff7e271
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="transaction-support-in-dbmss"></a>Dbms 中的交易支援
某些資料庫中，例如 dBASE、 Paradox 和 Btrieve，特別是桌面資料庫不支援交易。 支援交易的資料庫，之間，甚至沒有在不同的 SQL 陳述式可以是在交易中的變化。 如需詳細資訊，請參閱中的 SQL_TXN_CAPABLE 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。
