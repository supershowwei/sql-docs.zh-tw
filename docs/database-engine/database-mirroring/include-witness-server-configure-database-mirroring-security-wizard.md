---
title: "包含見證伺服器 (設定資料庫鏡像安全性精靈) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.configdbmsecurwiz.inclwitness.f1
ms.assetid: f04b38a4-f4e2-4d4c-bdac-7cc70e5a5684
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f3af2128d62e851e244509365504c361b596c5e5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="include-witness-server-configure-database-mirroring-security-wizard"></a>包含見證伺服器 (設定資料庫鏡像安全性精靈)
  使用此頁面，來指定您是否想要將見證伺服器包含在資料庫鏡像的這個安全性組態中。  
  
 **若要使用 SQL Server Management Studio 設定資料庫鏡像**  
  
-   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [啟動設定資料庫鏡像安全性精靈 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>選項  
 **是**  
 按一下即可將見證伺服器執行個體包含在安全性組態中。 具有自動容錯移轉的高安全性模式必須要有見證伺服器，如果主體伺服器執行個體失敗，這個見證伺服器就可以支援自動容錯移轉至鏡像伺服器執行個體。  
  
 **否**  
 按一下即可設定不具見證的安全性。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫屬性 &#40;鏡像頁面&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [資料庫鏡像見證](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  