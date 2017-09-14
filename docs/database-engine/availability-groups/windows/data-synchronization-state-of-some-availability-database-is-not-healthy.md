---
title: "某些可用性資料庫的資料同步處理狀態不健全 | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.drp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 89f95d15-33c6-4768-bccd-9dbf8c4f49a9
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 38a5c364965a31d1442ea68a982270b109aa3451
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="data-synchronization-state-of-some-availability-database-is-not-healthy"></a>某些可用性資料庫的資料同步處理狀態不健全
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性複本資料同步處理狀態|  
|**問題**|某個可用性資料庫的資料同步處理狀態不良。|  
|**類別目錄**|**警告**|  
|**Facet**|可用性複本|  
  
## <a name="description"></a>描述  
 此原則會檢查可用性資料庫 (也稱為「資料庫複本」) 的資料同步處理狀態。 當資料同步處理狀態為 NOT SYNCHRONIZING，或同步認可資料庫複本的狀態不是 SYNCHRONIZED 時，原則為狀況不良。  
  
> [!NOTE]  
>  在此 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]版本中，可能原因和解決方案的相關資訊位於 TechNet Wiki 上的 [Data synchronization state of availability database is not healthy](http://go.microsoft.com/fwlink/p/?LinkId=220863) (可用性資料庫的資料同步處理狀態不良)。  
  
## <a name="possible-causes"></a>可能的原因  
 複本上至少一個可用性資料庫有狀況不良的資料同步處理狀態。 如果這是非同步認可可用性複本，所有可用性資料庫都應該處於 SYNCHRONIZING 狀態。 如果這是同步認可可用性複本，所有可用性資料庫都應該處於 SYNCHRONIZED 狀態。 這個問題可能是由於下列原因所造成：  
  
-   可用性複本可能已中斷連接。  
  
-   資料移動可能已暫停。  
  
-   資料庫可能無法存取。  
  
-   可能由於網路延遲或主要或次要複本上的負載，發生短暫的延遲問題。  
  
## <a name="possible-solution"></a>可能的解決方案  
 解決任何連接或資料移動暫停問題。 使用 SQL Server Management Studio，檢查此問題的事件，並尋找資料庫錯誤。 依照特定錯誤的疑難排解步驟進行。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 Always On 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
