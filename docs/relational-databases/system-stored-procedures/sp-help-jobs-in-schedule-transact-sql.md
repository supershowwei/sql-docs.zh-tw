---
title: sp_help_jobs_in_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobs_in_schedule_TSQL
- sp_help_jobs_in_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobs_in_schedule
ms.assetid: 1168aa2c-136b-4ba3-b18e-9070d95a26fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0f892bf81811538eeb06b18feb725778464910b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528380"
---
# <a name="sphelpjobsinschedule-transact-sql"></a>sp_help_jobs_in_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回附加了特定排程之作業的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_jobs_in_schedule   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>引數  
`[ @schedule_id = ] schedule_id` 要列出資訊的排程識別碼。 *schedule_id*已**int**，沒有預設值。 任一*schedule_id*或是*schedule_name&lt*可能指定。  
  
`[ @schedule_name = ] 'schedule_name'` 要列出資訊的排程名稱。 *schedule_name&lt*已**sysname**，沒有預設值。 任一*schedule_id*或是*schedule_name&lt*可能指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 傳回下列結果集：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作業的唯一識別碼。|  
|**originating_server**|**nvarchar(30)**|作業的來源伺服器名稱。|  
|**name**|**sysname**|作業名稱。|  
|**enabled**|**tinyint**|指出是否啟用作業，以便執行。|  
|**description**|**nvarchar(512)**|作業的描述。|  
|**start_step_id**|**int**|應該作為執行起點的作業步驟識別碼。|  
|**category**|**sysname**|作業類別目錄。|  
|**owner**|**sysname**|作業擁有者。|  
|**notify_level_eventlog**|**int**|這是一個位元遮罩，指出在哪些情況之下，應該將通知事件記錄在 Microsoft Windows 應用程式記錄檔中。 它可以是下列值之一：<br /><br /> **0** = 永不<br /><br /> **1** = 當作業成功時<br /><br /> **2** = 當作業失敗時<br /><br /> **3** = 每當作業完成 （不論作業結果）|  
|**notify_level_email**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送通知電子郵件。 可能的值為相同**notify_level_eventlog**。|  
|**notify_level_netsend**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送網路訊息。 可能的值為相同**notify_level_eventlog**。|  
|**notify_level_page**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送頁面。 可能的值為相同**notify_level_eventlog**。|  
|**notify_email_operator**|**sysname**|要通知的操作員電子郵件名稱。|  
|**notify_netsend_operator**|**sysname**|傳送網路訊息時所用的電腦或使用者名稱。|  
|**notify_page_operator**|**sysname**|傳送呼叫時所用的電腦或使用者名稱。|  
|**delete_level**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時刪除作業。 可能的值為相同**notify_level_eventlog**。|  
|**date_created**|**datetime**|作業的建立日期。|  
|**date_modified**|**datetime**|上次修改作業的日期。|  
|**version_number**|**int**|作業的版本 (每次修改作業時，都會自動更新)。|  
|**last_run_date**|**int**|上次開始執行作業的日期。|  
|**last_run_time**|**int**|上次開始執行作業的時間。|  
|**last_run_outcome**|**int**|上次執行作業的輸出：<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **3** = 取消<br /><br /> **5** = 未知|  
|**next_run_date**|**int**|排程下一次執行作業的日期。|  
|**next_run_time**|**int**|排程下一次執行作業的時間。|  
|**next_run_schedule_id**|**int**|下次執行的排程識別碼。|  
|**current_execution_status**|**int**|目前的執行狀態。|  
|**current_execution_step**|**sysname**|作業中目前的執行步驟。|  
|**current_retry_attempt**|**int**|如果作業在執行中，且已重試這個步驟，這便是目前這次的重試。|  
|**has_step**|**int**|作業所擁有的作業步驟數目。|  
|**has_schedule**|**int**|作業所擁有的作業排程數目。|  
|**has_target**|**int**|作業所擁有的目標伺服器數目。|  
|**type**|**int**|作業類型：<br /><br /> **1** = 本機作業。<br /><br /> **2** = 多伺服器作業。<br /><br /> **0** = 作業已沒有目標伺服器。|  
  
## <a name="remarks"></a>備註  
 這個程序會列出附加至指定排程之作業的相關資訊。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 成員**SQLAgentUserRole**只能檢視他們擁有之作業的狀態。  
  
## <a name="examples"></a>範例  
 下列範例會列出附加至 `NightlyJobs` 排程的作業。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobs_in_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
