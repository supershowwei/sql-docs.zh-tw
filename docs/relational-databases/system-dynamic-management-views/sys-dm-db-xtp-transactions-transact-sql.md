---
title: sys.dm_db_xtp_transactions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_transactions
- sys.dm_db_xtp_transactions_TSQL
- dm_db_xtp_transactions
- dm_db_xtp_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_transactions dynamic management view
ms.assetid: 5c1a0a7a-e851-4b6f-8dfd-c9655fbf5a51
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e56e641a594d9a543c70485dc37daaf83f5e46f4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724173"
---
# <a name="sysdmdbxtptransactions-transact-sql"></a>sys.dm_db_xtp_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  報告記憶體中 OLTP 資料庫引擎中的使用中交易。  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
    
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|xtp_transaction_id|**bigint**|XTP 異動管理員中這項交易的內部識別碼。|  
|transaction_id|**bigint**|交易識別碼。 在其他交易相關 DMV 中透過交易識別碼聯結，例如 sys.dm_tran_active_transactions。<br /><br /> 0 代表僅限 XTP 交易，例如，原生編譯的預存程序啟動的交易。|  
|session_id|**smallint**|執行此交易之工作階段的工作階段識別碼。 與 sys.dm_exec_sessions 聯結。|  
|begin_tsn|**bigint**|交易的開始交易序號。|  
|end_tsn|**bigint**|交易的結束交易序號。|  
|state|**int**|交易的狀態：<br /><br /> 0=ACTIVE<br /><br /> 1=COMMITTED<br /><br /> 2=ABORTED<br /><br /> 3=VALIDATING|  
|state_desc|**nvarchar**|交易狀態的描述。|  
|result|**int**|此交易的結果。 以下是可能的值。<br /><br /> 0 - IN PROGRESS<br /><br /> 1 - SUCCESS<br /><br /> 2 - ERROR<br /><br /> 3 - COMMIT DEPENDENCY<br /><br /> 4 - VALIDATION FAILED (RR)<br /><br /> 5 - VALIDATION FAILED (SR)<br /><br /> 6 - ROLLBACK|  
|result_desc|**nvarchar**|此交易的結果。 以下是可能的值。<br /><br /> IN PROGRESS<br /><br /> SUCCESS<br /><br /> error<br /><br /> COMMIT DEPENDENCY<br /><br /> VALIDATION FAILED (RR)<br /><br /> VALIDATION FAILED (SR)<br /><br /> ROLLBACK|  
|last_error|**int**|僅供內部使用|  
|is_speculative|**bit**|僅供內部使用|  
|is_prepared|**bit**|僅供內部使用|  
|is_delayed_durability|**bit**|僅供內部使用|  
|memory_address|**varbinary**|僅供內部使用|  
|database_address|**varbinary**|僅供內部使用|  
|thread_id|**int**|僅供內部使用|  
|read_set_row_count|**int**|僅供內部使用|  
|write_set_row_count|**int**|僅供內部使用|  
|scan_set_count|**int**|僅供內部使用|  
|savepoint_garbage_count|**int**|僅供內部使用|  
|log_bytes_required|**bigint**|僅供內部使用|  
|count_of_allocations|**int**|僅供內部使用|  
|allocated_bytes|**int**|僅供內部使用|  
|reserved_bytes|**int**|僅供內部使用|  
|commit_dependency_count|**int**|僅供內部使用|  
|commit_dependency_total_attempt_count|**int**|僅供內部使用|  
|scan_area|**int**|僅供內部使用|  
|scan_area_desc|**nvarchar**|僅供內部使用|  
|scan_location|**int**|僅供內部使用。|  
|dependent_1_address|**varbinary(8)**|僅供內部使用|  
|dependent_2_address|**varbinary(8)**|僅供內部使用|  
|dependent_3_address|**varbinary(8)**|僅供內部使用|  
|dependent_4_address|**varbinary(8)**|僅供內部使用|  
|dependent_5_address|**varbinary(8)**|僅供內部使用|  
|dependent_6_address|**varbinary(8)**|僅供內部使用|  
|dependent_7_address|**varbinary(8)**|僅供內部使用|  
|dependent_8_address|**varbinary(8)**|僅供內部使用|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW DATABASE STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化的資料表動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
