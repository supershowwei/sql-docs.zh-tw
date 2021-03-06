---
title: sp_autostats & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_autostats_TSQL
- sp_autostats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_autostats
ms.assetid: d1df8c15-ee73-49eb-9d13-6e98943c3e38
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6264266f85edc1cae0821bbcf81c8c0993dba151
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62995696"
---
# <a name="spautostats-transact-sql"></a>sp_autostats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  顯示或變更索引、統計資料物件、資料表或索引檢視表的自動統計資料更新選項 AUTO_UPDATE_STATISTICS。  
  
 如需有關 AUTO_UPDATE_STATISTICS 選項的詳細資訊，請參閱 < [ALTER DATABASE SET 選項&#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)並[統計](../../relational-databases/statistics/statistics.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_autostats [ @tblname = ] 'table_or_indexed_view_name'   
    [ , [ @flagc = ] 'stats_value' ]   
    [ , [ @indname = ] 'statistics_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @tblname = ] 'table_or_indexed_view_name'` 資料表的名稱或索引檢視，要顯示 AUTO_UPDATE_STATISTICS 選項。 *table_or_indexed_view_name* is **nvarchar(776)**, with no default.  
  
`[ @flagc = ] 'stats_value'` AUTO_UPDATE_STATISTICS 選項更新這些值的其中一個：  
  
 **ON** = ON  
  
 **OFF** = OFF  
  
 當*stats_flag*是未指定，顯示目前的 AUTO_UPDATE_STATISTICS 設定。 *stats_value*已**varchar(10)**，預設值是 NULL。  
  
`[ @indname = ] 'statistics_name'` 是要顯示或更新 AUTO_UPDATE_STATISTICS 選項之統計資料名稱。 若要顯示索引的統計資料，您可以使用索引的名稱。索引及其對應的統計資料物件會具有相同的名稱。  
  
 *statistics_name*已**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 如果*stats_flag*指定，則**sp_autostats**報告的動作，擷取，但會傳回任何結果集。  
  
 如果*stats_flag*未指定，則**sp_autostats**會傳回下列結果集。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**Index Name**|**varchar(60)**|索引或統計資料的名稱。|  
|**AUTOSTATS**|**varchar(3)**|AUTO_UPDATE_STATISTICS 選項的目前值。|  
|**上次更新日期**|**datetime**|最近更新統計資料的日期。|  
  
 在結果集的資料表或索引檢視表包含建立索引，使用 AUTO_CREATE_STATISTICS 選項所產生的單一資料行統計資料的統計資料，並使用所建立的統計資料[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)陳述式。  
  
## <a name="remarks"></a>備註  
 如果停用了指定的索引，或指定的資料表具有停用的叢集索引，就會顯示一則錯誤訊息。  
  
 如果是記憶體最佳化的資料表，AUTO_UPDATE_STATISTICS 永遠都是 OFF。  
  
## <a name="permissions"></a>Permissions  
 若要變更 AUTO_UPDATE_STATISTICS 選項，您需要**db_owner**固定資料庫角色或 ALTER 權限*table_name*。若要顯示 AUTO_UPDATE_STATISTICS 選項需要的成員資格**公開**角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-display-the-status-of-all-statistics-on-a-table"></a>A. 顯示資料表上所有統計資料的狀態  
 下列範例會顯示 `Product` 資料表上所有統計資料的狀態。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product';  
GO  
```  
  
### <a name="b-enable-autoupdatestatistics-for-all-statistics-on-a-table"></a>B. 針對資料表的所有統計資料啟用 AUTO_UPDATE_STATISTICS  
 下列範例會針對 `Product` 資料表的所有統計資料啟用 AUTO_UPDATE_STATISTICS 選項。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'ON';  
GO  
```  
  
### <a name="c-disable-autoupdatestatistics-for-a-specific-index"></a>C. 針對特定索引停用 AUTO_UPDATE_STATISTICS  
 下列範例會針對 `AK_Product_Name` 資料表的 `Product` 索引停用 AUTO_UPDATE_STATISTICS 選項。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'OFF', AK_Product_Name;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [統計資料](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
