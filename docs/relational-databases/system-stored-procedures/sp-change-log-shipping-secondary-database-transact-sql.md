---
title: sp_change_log_shipping_secondary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 136771c5bf691155b4547963fa2b6bd035f3f039
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62994227"
---
# <a name="spchangelogshippingsecondarydatabase-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更次要資料庫設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>引數  
`[ @restore_delay = ] 'restore_delay'` 以分鐘為單位，次要伺服器還原指定的備份檔之前等待的時間量。 *restore_delay*已**int**不能是 NULL。 預設值為 0。  
  
`[ @restore_all = ] 'restore_all'` 如果設定為 1，次要伺服器還原所有可用的交易記錄備份，當執行還原作業。 否則，它會在還原一個檔案之後停止。 *restore_all*已**元**不能是 NULL。  
  
`[ @restore_mode = ] 'restore_mode'` 次要資料庫的還原模式。  
  
 0 = 以 NORECOVERY 來還原記錄。  
  
 1 = 以 STANDBY 來還原記錄。  
  
 *還原*已**元**不能是 NULL。  
  
`[ @disconnect_users = ] 'disconnect_users'` 如果設定為 1，使用者已在執行還原作業時，從次要資料庫中斷連接。 預設值 = 0。 *disconnect_users*已**元**不能是 NULL。  
  
`[ @block_size = ] 'block_size'` 大小 （位元組），做為備份裝置區塊大小。 *block_size*已**int**預設值為-1。  
  
`[ @buffer_count = ] 'buffer_count'` 備份或還原作業所用的緩衝區總數。 *buffer_count*已**int**預設值為-1。  
  
`[ @max_transfer_size = ] 'max_transfer_size'` 大小，以位元組為單位的最大輸入或輸出要求由發行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]向備份裝置。 *max_transfersize*已**int**而且可以是 NULL。  
  
`[ @restore_threshold = ] 'restore_threshold'` 在產生警示之前，之間所能經歷的分鐘數會還原作業。 *restore_threshold*已**int**不能是 NULL。  
  
`[ @threshold_alert = ] 'threshold_alert'` 是當超出還原臨界值時產生警示。 *threshold_alert*已**int**，預設值是 14420。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` 指定是否可以警示時引發*restore_threshold*超過。 1 = 已啟用；0 = 已停用。 *threshold_alert_enabled*已**元**不能是 NULL。  
  
`[ @history_retention_period = ] 'history_retention_period'` 這是時間的以分鐘為單位中保留記錄長度。 *history_retention_period*已**int**。如果未指定，會使用 1440年的數值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_change_log_shipping_secondary_database**必須從執行**主要**次要伺服器上的資料庫。 這個預存程序會執行下列動作：  
  
1.  在設定的變更**log_shipping_secondary_database**記錄。  
  
2.  變更中的之本機監視記錄**log_shipping_monitor_secondary**次要伺服器上使用提供的引數，如有必要。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="examples"></a>範例  
 此範例說明如何利用**sp_change_log_shipping_secondary_database**更新資料庫的次要資料庫參數**LogShipAdventureWorks**。  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
