---
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c32441ebcf8804f712fad3061bbd380864db3426
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62916297"
---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|10507|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_STMT_DOES_NOT_MATCH|  
|訊息文字|無法建立計畫指南 ' %。\*ls' 因為指定的陳述式`@stmt`並`@module_or_batch`，或由`@plan_handle`和`@statement_start_offset`、 不符合所指定模組中的任何陳述式或批次。 請將值修改為與模組或批次中的陳述式相符。|  
  
## <a name="explanation"></a>說明  
 指定之模組或批次中的陳述式無法與指定的陳述式或陳述式位移值相符。  
  
## <a name="user-action"></a>使用者動作  
 請將指定的參數值修改為與模組或批次中的陳述式相符。  
  
## <a name="see-also"></a>另請參閱  
 [計畫指南](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
