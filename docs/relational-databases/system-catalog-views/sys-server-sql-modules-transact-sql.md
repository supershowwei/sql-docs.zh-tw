---
title: sys.server_sql_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 95583de206841bb3ed3ccff42809c028443c63ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743950"
---
# <a name="sysserversqlmodules-transact-sql"></a>sys.server_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 TR 類型伺服器層級觸發程序的 SQL 模組集。 您可以將這個關聯性聯結到 sys.server_triggers。 Tuple (object_id) 是關聯性的索引鍵。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|這是對定義這個模組的伺服器層級觸發程序的 FOREIGN KEY 參考。|  
|**definition**|**nvarchar(max)**|定義這個模組的 SQL 文字。<br /><br /> NULL = 已加密。|  
|**uses_ansi_nulls**|**bit**|建立模組時，是將 ANSI NULLS 設定選項設為 ON。|  
|**uses_quoted_identifier**|**bit**|建立模組時，是將 QUOTED IDENTIFIER 設定選項設為 ON。|  
|**execute_as_principal_id**|**int**|EXECUTE AS 伺服器主體的識別碼。<br /><br /> 在預設或 EXECUTE AS CALLER 的情況下為 NULL。<br /><br /> 指定的主體 if 的識別碼執行 AS SELF EXECUTE AS 主體-2 = EXECUTE AS OWNER。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
