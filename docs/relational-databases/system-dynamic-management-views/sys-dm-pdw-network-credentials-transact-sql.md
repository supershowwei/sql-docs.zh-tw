---
title: sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7d9e18284ac4d97efaa217802682fe79ebb2dfc5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041519"
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  傳回一份所有的網路認證儲存在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置的所有目標伺服器。 結果會列出的控制節點和每個計算節點。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。|  
|target_server_name|**nvarchar(32)**|目標伺服器的 IP 位址，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會使用使用者名稱和密碼的認證來存取。|  
|username|**nvarchar(32)**|密碼會儲存使用者名稱。|  
|last_modified|**datetime**|修改認證的上次作業的日期時間。|  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW SERVER STATE。  
  
## <a name="general-remarks"></a>一般備註  
 這個動態管理檢視的索引鍵是*pdw_node_id*加上*target_server_name*。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
