---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e18232c9d45b9552bbb1c8a194d1dbb1f74878f7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915649"
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1458|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_FAILREDO_ON_PRIMARY|  
|訊息文字|'%.*ls' 資料庫的主體副本發現錯誤 %d，狀態 %d，嚴重性 %d。 資料庫鏡像已暫停。 請嘗試解決錯誤狀況，然後繼續執行鏡像。|  
  
## <a name="explanation"></a>說明  
 這個訊息表示主體資料庫遭遇錯誤，導致資料庫鏡像暫停。  
  
## <a name="user-action"></a>使用者動作  
 在大部分情況下，這個錯誤都會自動修正。 如果問題持續發生，重新啟動資料庫或伺服器執行個體通常就能修正問題。 如需詳細資訊，請查看每個夥伴的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以取得在此訊息之前發生的相關錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
