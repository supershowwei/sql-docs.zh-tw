---
title: 從移轉的必要條件是記錄傳送至 AlwaysOn 可用性群組 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 865e8d720e9977f582ac5ae8a0e75d995fc82629
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62789548"
---
# <a name="prerequisites-for-migrating-from-log-shipping-to-alwayson-availability-groups-sql-server"></a>從記錄傳送移轉至 AlwaysOn 可用性群組的必要條件 (SQL Server)
  本主題描述將記錄傳送主要資料庫與其一個或多個次要資料庫轉換成 AlwaysOn 主要資料庫和次要資料庫的必要條件。  
  
> [!NOTE]  
>  您可以將可用性群組中的任何主要或次要資料庫 (可能是可讀取) 設定為記錄傳送主要資料庫。  
  
 **本主題內容：**  
  
-   [可用性群組必要條件](#AGPrereqsRealAddress)  
  
-   [記錄傳送必要條件](#LogShipPrereqs)  
  
-   [相關工作](#RelatedTasks)  
  
-   [相關內容](#RelatedContent)  
  
##  <a name="AGPrereqsRealAddress"></a> 可用性群組必要條件  
 若要允許備份作業在可用性群組的主要複本上執行，請使用下列 AlwaysOn 可用性群組備份設定：  
  
|屬性|設定|  
|--------------|-------------|  
|可用性群組的自動備份喜好設定|只在主要複本上|  
|主要複本的備份優先權。|>0|  
  
 **如需詳細資訊：＜＞**  
  
 [檢視可用性群組屬性 &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
 [設定可用性複本的備份 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="LogShipPrereqs"></a> 記錄傳送必要條件  
  
-   記錄傳送主要資料庫必須位於主控可用性群組之初始/目前主要複本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上。  
  
-   為了將指定的記錄傳送次要資料庫轉換成 AlwaysOn 次要資料庫，它必須：  
  
    -   使用與主要資料庫相同的名稱。  
  
    -   位於主控可用性群組之次要複本的伺服器執行個體上。  
  
 備份作業在主要資料庫上執行之後，請停用備份作業；還原作業在指定的次要資料庫上執行之後，請停用還原作業。  
  
 為可用性群組建立所有次要資料庫之後，如果您想要在次要複本上執行備份，則需要重新設定可用性群組的自動備份喜好設定。  
  
 **如需詳細資訊：＜＞**  
  
 [Converting a logshipping configuration to Availability Group](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx) (將記錄傳送組態轉換成可用性群組) (SQL Server 部落格)  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **記錄傳送**  
  
-   [升級記錄傳送到 SQL Server 2014 &#40;Transact SQL&#41;](../../log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [移除記錄傳送 &#40;SQL Server&#41;](../../log-shipping/remove-log-shipping-sql-server.md)  
  
 **AlwaysOn 可用性群組**  
  
-   [使用可用性群組精靈 &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [建立可用性群組 &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [建立可用性群組 &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [設定可用性複本的備份 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   **部落格：**  
  
     [Converting a logshipping configuration to Availability Group](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx)  
  
     [將記錄傳送主要資料庫和次要資料庫加入至現有的可用性群組](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/01/use-log-shipping-to-prepare-secondary-databases-for-an-existing-availability-group.aspx)  
  
     [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程師部落格](https://blogs.msdn.com/b/psssql/)  
  
-   **白皮書：**  
  
     [Migration Guide:移轉至 AlwaysOn 可用性群組從先前的部署結合資料庫鏡像與記錄傳送](https://msdn.microsoft.com/library/jj635217)  
  
     [Microsoft 的 SQL Server 2012 白皮書](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客戶諮詢團隊白皮書](http://sqlcat.com/)  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../log-shipping/about-log-shipping-sql-server.md)   
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [監視可用性群組 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
