---
title: catalog.update_logdb_info (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
author: haoqian
ms.author: haoqian
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 2df4819b14c1dec7aa1203d0a4c3416b59f292e0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830756"
---
# <a name="catalogupdatelogdbinfo-ssisdb-database"></a>catalog.update_logdb_info (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 記錄資訊。

## <a name="syntax"></a>語法

```sql
catalog.update_logdb_info [@server_name = ] server_name, [@connection_string = ] connection_string
```

## <a name="arguments"></a>引數
[ @server_name = ] *server_name*  
 用於 Scale Out 記錄的 SQL Server。 *server_name* 是 **nvarchar**。  

 [ @connection_string = ] *connection_string*  
 用於 Scale Out 記錄的連接字串。 *connection_string* 是 **nvarchar**。

 ## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  

## <a name="permissions"></a>[權限]  
 這個預存程序需要下列其中一個權限：  
   
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
 
