---
title: 升級 PowerPivot for SharePoint |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80ba9e43-f3f0-4730-9fb1-2afd2dd3e6fc
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de63ecc80b175385846845f5901fde5eb37ec97c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775644"
---
# <a name="upgrade-powerpivot-for-sharepoint"></a>升級 PowerPivot for SharePoint
  本主題概述將 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 部署升級至 [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)]所需的步驟。 特定步驟取決於您環境目前所執行的 SharePoint 版本，並包含 PowerPivot for SharePoint 增益集 (**spPowerPivot.msi**)。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 | SharePoint 2013  
  
 如需版本資訊，請參閱＜ [SQL Server 2014 版本資訊](https://go.microsoft.com/fwlink/?LinkID=296445)＞。  
  

  
## <a name="background"></a>背景  
  
-   如果您要升級含有兩個 (含) 以上 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 執行個體的多伺服器 SharePoint 2010 伺服器陣列，必須在繼續升級下一部伺服器 **之前** ，完整升級每部伺服器。 完整升級包括執行 SQL Server 安裝程式來升級 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 程式檔案，然後再執行 SharePoint 升級動作來設定已升級的服務。 在適當的 PowerPivot 組態工具或 Windows PowerShell 中執行升級動作之前，伺服器可用性會受到限制。  
  
-   SharePoint 2010 伺服陣列中的所有 PowerPivot 系統服務與 Analysis Services 執行個體都必須是相同的版本。 如需有關如何驗證版本的詳細資訊，請參閱本主題中的 [驗證 PowerPivot 元件和服務的版本](#bkmk_verify_versions) 一節。  
  
-   PowerPivot 組態工具是 SQL Server 共用功能之一，所有共用功能都會同時升級。 如果您在升級過程中選取需要共用功能升級的其他 SQL Server 執行個體或功能，則 PowerPivot 組態工具也會一併升級。 如果升級 PowerPivot 組態工具但是未升級 PowerPivot 執行個體，可能會發生問題。 如需有關 SQL Server 共用功能的詳細資訊，請參閱 <<c0> [ 升級到使用的 SQL Server 2014 安裝精靈&#40;安裝&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)。</c0>  
  
-   PowerPivot for SharePoint 增益集 (**spPowerPivot.msi**) 會與舊版並排安裝。 例如， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 增益集會安裝至資料夾 `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools`。  
  

  
##  <a name="bkmk_prereq"></a> 必要條件  
 **Permissions**  
  
-   您必須是伺服器陣列管理員，才能升級 PowerPivot for SharePoint 安裝。 您必須是本機系統管理員，才能執行 SQL Server 安裝程式。  
  
-   您必須要有伺服器陣列組態資料庫的 **db_owner** 權限。  
  
 **SQL Server:**  
  
-   如果現有的 PowerPivot 安裝為 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]，則需要 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Service Pack 2 (SP2)，才能升級至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。  
  
-   如果現有的 PowerPivot 安裝為 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，則需要 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 (SP1)，才能升級至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。  
  
 **SharePoint 2010：**  
  
-   如果現有的安裝是執行 SharePoint 2010，請先安裝 SharePoint 2010 Service Pack 2，再升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。 如需詳細資訊，請參閱＜ [Service Pack 2 for Microsoft SharePoint 2010](https://www.microsoft.com/download/details.aspx?id=39672)＞。 使用 PowerShell 命令 `(Get-SPfarm).BuildVersion.ToString()` 來驗證版本。 若要將組建版本參照至發行日期，請參閱＜ [SharePoint 2010 組建編號](http://www.toddklindt.com/blog/Lists/Posts/Post.aspx?ID=224)＞。  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2013"></a> 升級現有的 SharePoint 2013 伺服器陣列  
 若要將部署在 SharePoint 2013 中的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 升級，請執行下列動作：  
  
 ![PowerPivot for SharePoint 2013 升級](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2013.png "PowerPivot for SharePoint 2013 升級")  
  
1.  在以 SharePoint 模式執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的後端伺服器上，執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安裝程式。 如果該伺服器主控多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體，則至少要升級 **POWERPIVOT** 執行個體。 下列清單是有關 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 升級的安裝精靈步驟摘要：  
  
    1.  在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈] 中，按一下 **[安裝]**。  
  
    2.  按一下 [從 SQL Server 升級...]。  
  
    3.  在 **[選取執行個體]** 頁面上，選取 **[POWERPIVOT]** 執行個體名稱，然後按 **[下一步]**。  
  
    4.  如需詳細資訊，請參閱 <<c0> [ 升級到使用的 SQL Server 2014 安裝精靈&#40;安裝程式&#41;</c0>](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
2.  重新啟動伺服器。  
  
3.  在 SharePoint 2013 伺服器陣列中的每部伺服器上，執行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 增益集 (**spPowerPivot.msi**)，以安裝資料提供者。 但是執行 SQL Server 安裝精靈所在的伺服器除外，安裝精靈也會升級資料提供者。 如需詳細資訊，請參閱 <<c0> [ 安裝或解除安裝 PowerPivot for SharePoint 增益集&#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。</c0>  
  
4.  在其中一個 SharePoint 應用程式伺服器上**執行 PowerPivot for SharePoint 2013 組態** 工具，以增益集所安裝的更新方案檔案來設定 SharePoint 伺服器陣列。 您無法使用 SharePoint 管理中心來進行此步驟。 如需詳細資訊，請參閱下列內容：  
  
    1.  在 Windows 的 [開始] 頁面中，輸入 **PowerPivot** ，然後在搜尋結果中，按一下 **[PowerPivot for SharePoint 2013 組態]**。 請注意，搜尋可能會將組態工具的兩個版本皆傳回。  
  
         ![兩個 PowerPivot 組態工具](../../../2014/analysis-services/media/as-powerpivot-configtools-bothicons.gif "兩個 PowerPivot 組態工具")  
  
         或  
  
         在 **[開始]** 功能表上，指向 **[所有程式]**，然後依序按一下 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[組態工具]** 和 **[PowerPivot for SharePoint 2013 組態工具]**。 請注意，只有在本機伺服器上安裝了 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 時，才會列出此工具。  
  
    2.  啟動時，組態工具會檢查 PowerPivot 伺服器陣列方案以及 PowerPivot Web 應用程式方案的狀態。 如果偵測到這些解決方案的較舊版本，您會看到訊息 「**已偵測到較新版本的 PowerPivot 方案檔。請選取升級選項以升級您的伺服器陣列**」。 按一下 [確定]  以關閉系統驗證訊息。  
  
    3.  按一下 **[升級功能、服務、應用程式和方案]**，然後按一下 **[確定]**。  
  
    4.  檢閱左窗格工作清單中的動作，並排除您不希望該工具執行的任何動作。 預設包含所有動作。 若要移除動作，請在左邊工作清單中選取該動作，然後清除 **[參數]** 頁面上的 **[在工作清單中包含這個動作]** 核取方塊。  
  
    5.  或者，在 **[指令碼]** 或 **[輸出]** 索引標籤中檢閱詳細資訊。  
  
         [輸出] 索引標籤是此工具即將執行之動作的摘要。 此資訊會儲存在記錄檔中： `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`。  
  
         [指令碼] 索引標籤會顯示 PowerShell 指令程式，或參考此工具將執行的 PowerShell 指令碼檔案。  
  
    6.  按一下 **[驗證]** 來檢查每個動作是否有效。 如果無法使用 **[驗證]** ，表示所有動作都適用於您的系統。 如果可以使用 **[驗證]** ，表示您可能已經修改輸入值 (例如，Excel 服務應用程式名稱)，或此工具可能已經判定府執行特定動作。 如果無法執行某個動作，您必須排除該動作，或修正造成此動作標示為無效的基礎條件。  
  
        > [!IMPORTANT]  
        >  您必須一律先處理第一個動作 **[升級伺服器陣列方案]**。 此動作會註冊用來設定伺服器的 PowerShell 指令程式。 如果此動作出現錯誤，請不要繼續。 在處理工作清單中的其他動作之前，請改用此錯誤所提供的資訊診斷並解決問題。  
  
    7.  按一下 **[執行]** ，執行適用於此工作的所有動作。 只有在通過驗證檢查的情況下，才可以使用 **[執行]** 。 當您按一下 [執行] 時，會出現下列警告，提醒您動作是在批次模式下處理：「**工具中標示為有效的所有組態設定都會套用到 SharePoint 伺服器陣列。您要繼續嗎？**」  
  
    8.  按一下 **[是]** 繼續。  
  
    9. 在伺服器陣列中升級方案和功能可能需要數分鐘才能完成。 在此期間，連接要求 PowerPivot 資料**將會失敗**具有類似的錯誤 」**無法重新整理資料**「 或 」**嘗試執行要求的動作時發生錯誤。請再試一次**」。 升級完成後，伺服器將會變成可以使用，而且將不再發生這些錯誤。  
  
     如需詳細資訊，請參閱下列內容：  
  
    -   [PowerPivot 設定工具](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
    -   [設定或修復 PowerPivot for SharePoint 2013 &#40;PowerPivot 組態工具&#41;](../../analysis-services/power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md)  
  
    -   [使用 Windows PowerShell 的 PowerPivot 設定](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
    -   [Powerpivot for SharePoint 的 PowerShell 參考](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
5.  透過執行升級後的步驟以及檢查伺服器陣列中的 PowerPivot 伺服器版本，驗證升級成功。 如需詳細資訊，請參閱本主題中的 [Post-upgrade verification tasks](#verify) 和下列章節：  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2010"></a> 升級現有的 SharePoint 2010 伺服器陣列  
 若要將部署在 SharePoint 2010 中的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 升級，請執行下列動作：  
  
 ![PowerPivot for SharePoint 2010 升級](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2010.png "PowerPivot for SharePoint 2010 升級")  
  
1.  下載 [Service Pack 2 for Microsoft SharePoint 2010](https://www.microsoft.com/download/details.aspx?id=39672) ，並套用至伺服器陣列中的所有伺服器。 確認 SharePoint SP2 安裝成功。 在管理中心的 [升級與移轉] 頁面上，開啟 [檢查產品與修補安裝狀態] 頁面，以檢視與 SP2 相關的狀態訊息。  
  
2.  確認 SharePoint 2010 Administration Windows 服務正在執行中。  
  
    ```  
    Get-Service | where {$_.displayname -like "*SharePoint*"}  
    ```  
  
3.  確認 SharePoint 管理中心已經啟動 **SharePoint** 服務、 **SQL Server Analysis Services** 和 **SQL Server PowerPivot 系統服務** ，或使用下列 PowerShell 命令：  
  
    ```  
    get-SPserviceinstance | where {$_.typename -like "*sql*"}  
    ```  
  
4.  確認 **Windows** 服務 **SQL Server Analysis Services (PowerPivot)** 執行中。  
  
    ```  
    Get-Service | where {$_.displayname -like "*powerpivot*"}  
    ```  
  
5.  **在以 SharePoint 模式執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SQL Server Analysis Services (PowerPivot)** Windows 服務的第一部 SharePoint 應用程式伺服器上， **SQL Server Analysis Services (PowerPivot)** ，以升級 POWERPIVOT 執行個體。 在 [SQL Server 安裝精靈] 的 [安裝] 頁面上，選擇升級選項。 如需詳細資訊，請參閱 <<c0> [ 升級到使用的 SQL Server 2014 安裝精靈&#40;安裝&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)。</c0>  
  
6.  在執行組態工具之前，請先**重新啟動伺服器** 。 此步驟可確保 SQL Server 安裝程式安裝的任何更新或必要條件完全在系統上設定。  
  
7.  **執行 PowerPivot 組態工具**第一部 SharePoint 應用程式伺服器在 SharePoint 中執行 SQL Server Analysis Services (PowerPivot) 服務，若要升級方案和 Web 服務。 您無法使用管理中心進行此步驟。  
  
    1.  指向 **[開始]** 功能表上的 **[所有程式]**，按一下 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]，然後按一下 **[組態工具]**，再按一下 **[PowerPivot 組態工具]**。 請注意，只有在本機伺服器上安裝了 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 時，才會列出此工具。  
  
    2.  啟動時，組態工具會檢查 PowerPivot 伺服器陣列方案以及 PowerPivot Web 應用程式方案的狀態。 如果偵測到這些解決方案的較舊版本，您會看到訊息 「 有已偵測到較新版本的 PowerPivot 方案檔。 請選取升級選項以升級您的伺服器陣列」。 按一下 **[確定]** 以關閉訊息。  
  
    3.  按一下 **[升級功能、服務、應用程式和方案]**，然後按一下 **[確定]** 繼續。  
  
    4.  出現下列警告：「 PowerPivot 管理儀表板中的活頁簿即將升級為最新版本。 您對現有活頁簿所做的任何自訂內容都將遺失。 您要繼續嗎？」  
  
         此警告指的是 PowerPivot 管理儀表板中，針對資料重新整理活動報告的活頁簿。 如果您自訂這些活頁簿，當現有的檔案取代成較新的版本時，您對這些活頁簿所做的任何變更都會遺失。  
  
         按一下 **[是]** ，將活頁簿覆寫成較新的版本。 否則，按一下 **[否]** ，返回首頁。 將活頁簿儲存到不同的位置，讓您擁有一個副本，然後在準備好繼續時，返回此步驟。  
  
         如需有關自訂儀表板中使用之活頁簿的詳細資訊，請參閱 [自訂 PowerPivot 管理儀表板](https://go.microsoft.com/fwlink/?linkID=229639)。  
  
    5.  檢閱工作清單中的動作，並排除您不希望該工具執行的任何動作。 預設包含所有動作。 若要移除動作，請在工作清單中選取該動作，然後清除 [參數] 頁面上的 **[在工作清單中包含這個動作]** 核取方塊。  
  
    6.  或者，在 **[輸出]** 索引標籤或 **[指令碼]** 索引標籤中檢閱詳細資訊。  
  
         [輸出] 索引標籤是此工具即將執行之動作的摘要。 此資訊會儲存在記錄檔中： `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Log`。  
  
         [指令碼] 索引標籤會顯示 PowerShell 指令程式，或參考此工具將執行的 PowerShell 指令碼檔案。  
  
    7.  按一下 **[驗證]** 來檢查每個動作是否有效。 如果無法使用 **[驗證]** ，表示所有動作都適用於您的系統。 如果可以使用 **[驗證]** ，表示您可能已經修改輸入值 (例如，Excel 服務應用程式名稱)，或此工具可能已經判定府執行特定動作。 如果無法執行某個動作，您必須排除該動作，或修正造成此動作標示為無效的基礎條件。  
  
        > [!IMPORTANT]  
        >  您必須一律先處理第一個動作 **[升級伺服器陣列方案]**。 此動作會註冊用來設定伺服器的 PowerShell 指令程式。 如果此動作出現錯誤，請不要繼續。 在處理工作清單中的其他動作之前，請改用此錯誤所提供的資訊診斷並解決問題。  
  
    8.  按一下 **[執行]** ，執行適用於此工作的所有動作。 只有在通過驗證檢查的情況下，才可以使用 **[執行]** 。 當您按一下 [執行] 時，會出現下列警告，提醒您動作是在批次模式下處理：「工具中標示為有效的所有組態設定都會套用到 SharePoint 伺服器陣列。 您要繼續嗎？」  
  
    9. 按一下 **[是]** 繼續。  
  
    10. 在伺服器陣列中升級方案和功能可能需要數分鐘才能完成。 在此期間，PowerPivot 資料連接要求將會失敗並出現 「 無法重新整理資料 」 或者 「 錯誤時發生嘗試執行要求的動作。 請再試一次」。 升級完成後，伺服器將會變成可以使用，而且將不再發生這些錯誤。  
  
8.  **重複此程序**伺服陣列中每個 SQL Server Analysis Services (PowerPivot) 服務：1） 執行 SQL Server 安裝程式 2） 執行 PowerPivot 組態工具。  
  
9. 透過執行升級後的步驟以及檢查伺服器陣列中的 PowerPivot 伺服器版本，驗證升級成功。 如需詳細資訊，請參閱本主題中的 [Post-upgrade verification tasks](#verify) 和下列章節：  
  
10. **疑難排解錯誤**  
  
     您可以在 [參數] 窗格中檢視每個動作的錯誤資訊。  
  
     針對與方案部署或撤銷相關的問題，請確認已啟動 SharePoint 2010 Administrator 服務。 此服務會執行觸發伺服器陣列中組態變更的計時器作業。 如果該服務未執行，方案部署或撤銷將會失敗。 持續性錯誤指的是現有的部署或撤銷作業已經在佇列中，因此會攔截組態工具的其他動作。  
  
    1.  以管理員身分啟動 SharePoint 2010 管理命令介面，然後執行下列命令來檢視佇列中的作業：  
  
        ```  
        Stsadm -o enumdeployments  
        ```  
  
    2.  檢閱現有部署中的下列資訊：[類型] 是 [撤銷] 或 [部署]、[檔案] 是 powerpivotwebapp.wsp 或 powerpivotfarm.wsp。  
  
    3.  部署或撤銷與 PowerPivot 方案相關將複製的 GUID 值**JobId**然後將它貼到下列命令 （使用標記]、 [複製] 和 [貼上命令殼層的 [編輯] 功能表上來複製 GUID）：  
  
        ```  
        Stsadm -o canceldeployment -id "<GUID>"  
        ```  
  
    4.  依序按一下 **[驗證]** 和 **[執行]**，重試組態工具中的工作。  
  
     至於其他所有錯誤，請檢查 ULS 記錄檔。 如需詳細資訊，請參閱 <<c0> [ 設定及檢視 SharePoint 記錄檔和診斷記錄&#40;PowerPivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)。</c0>  
  

  
##  <a name="bkmk_workbooks"></a> 活頁簿  
 升級伺服器不一定會升級伺服器上執行的 PowerPivot 活頁簿，但是使用舊版 PowerPivot for Excel 建立的舊活頁簿仍可如常運作，並使用該版提供的功能。 活頁簿可以維持運作，是由於已升級的伺服器具有屬於舊版安裝的 Analysis Services OLE DB 提供者版本所致。  
  
  
  
##  <a name="bkmk_datarefresh"></a> 資料重新整理  
 升級會影響資料重新整理作業。 伺服器的排程資料重新整理僅適用於符合伺服器版本的活頁簿。 如果您裝載舊版的活頁簿，資料重新整理可能不再適用於這些活頁簿。 若要重新啟用資料重新整理，您必須升級活頁簿。 您可以在 PowerPivot for Excel 中升級每個活頁簿，或是針對 SharePoint 2010 中的資料重新整理功能啟用自動升級。 自動升級會在執行資料重新整理之前將活頁簿升級為最新版本，讓資料重新整理作業依排程執行。  
  

  
##  <a name="bkmk_verify_versions"></a> 驗證 PowerPivot 元件和服務的版本  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務和 Analysis Services 的所有執行個體必須是相同版本。 若要確認所有伺服器元件都是相同的版本，請檢查以下版本資訊：  
  
### <a name="verify-the-version-of-powerpivot-solutions-and-the-powerpivot-system-service"></a>驗證 PowerPivot 方案和 PowerPivot 系統服務的版本  
 執行下列 PowerShell 命令：  
  
```  
Get-PowerPivotSystemService  
```  
  
 驗證 **CurrentSolutionVersion**。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 是 12.0 版。\<主要組建 >。\<次要組建 >  
  
### <a name="verify-the-version-of-the-analysis-services-windows-service"></a>驗證 Analysis Services Windows 服務的版本  
 如果您只有升級 SharePoint 2010 伺服陣列中的部分 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 伺服器，則未升級之伺服器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體將會比預期在伺服器陣列中的版本還舊。 您必須將所有的伺服器升級至相同版本，才可以加以使用。 若要確認在每部電腦上的 SQL Server Analysis Services (PowerPivot) Windows 服務版本中使用下列方法之一。  
  
 **Windows 檔案總管**：  
  
1.  瀏覽至 **Bin** 資料夾，尋找 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 執行個體。 例如 `C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\bin`。  
  
2.  以滑鼠右鍵按一下 `msmdsrv.exe`，然後選取 **[屬性]**。  
  
3.  按一下 **[詳細資料]**。  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 檔案版本應為 12.00。\<主要組建 >。\<次要組建 >。  
  
5.  驗證這個編號與 PowerPivot 方案和系統服務版本相同。  
  
 **服務啟動資訊：**  
  
 當 PowerPivot 服務啟動時，會將版本資訊寫入至 Windows 事件記錄檔。  
  
1.  執行 Windows `eventvwr`  
  
2.  建立來源 `MSOLAP$POWERPIVOT`的篩選。  
  
3.  尋找類似下列的資訊層級事件  
  
     服務已啟動。 Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM **12.0.2000.8**。  
  
 **使用 PowerShell 來驗證檔案版本。**  
  
 您可以使用 PowerShell 來驗證產品版本。 如果您想要編寫指令碼或自動化版本驗證，PowerShell 是個好選項。  
  
```  
(get-childitem "C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe").VersionInfo  
```  
  
 上述 PowerShell 命令會傳回類似下列資訊：  
  
 ProductVersion   FileVersion           FileName  
  
 **12.0.2000.8** 2014.0120.200    C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe  
  
### <a name="verify-the-msolap-data-provider-version-on-sharepoint"></a>驗證 SharePoint 上的 MSOLAP 資料提供者版本  
 使用下列指示即可查看 Excel Services 信任的 Analysis Services OLE DB 提供者版本。 您必須是伺服陣列或服務應用程式系統管理員，才能檢查 Excel Services 信任的資料提供者設定。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
2.  按一下 Excel Services 服務應用程式的名稱，例如 **[ExcelServiceApp1]**。  
  
3.  按一下 **[信任的資料提供者]**。 您應該會看到 MSOLAP.5 (Microsoft OLE DB Provider for OLAP Services 11.0)。 如果您已升級 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安裝，也會看到舊版的 MSOLAP.4。  
  
4.  如需詳細資訊，請參閱＜ [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)＞。  
  
 MSOLAP.4 會描述為 Microsoft OLE DB Provider for OLAP Services 10.0。 這個版本可能是與 Excel Services 一併安裝的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 預設版本，或者是 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本。 SharePoint 安裝的預設版本不支援 PowerPivot 資料存取。 您必須擁有 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本或更新的版本，才能連接 SharePoint 上的 PowerPivot 活頁簿。 若要確認您擁有 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本，請使用上一節中說明如何檢視檔案屬性以確認版本的指示。  
  
### <a name="verify-the-adomdnet-data-provider-version"></a>驗證 ADOMD.NET 資料提供者版本  
 使用下列指示來檢查所安裝的 ADOMD.NET 版本。 您必須是伺服陣列或服務應用程式系統管理員，才能檢查 Excel Services 信任的資料提供者設定。  
  
1.  在 SharePoint 應用程式伺服器上，瀏覽至 `c:\Windows\Assembly`。  
  
2.  依組件名稱排序，並搜尋 **Microsoft.Analysis Services.Adomd.Client**。  
  
3.  請確認您有 12.0 版。\<組建編號 >。  
  
  
  
##  <a name="geminifarm"></a> 升級多部 PowerPivot for SharePoint 伺服器陣列中的 SharePoint 伺服器  
 在包含多部 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 伺服器的多重伺服器拓撲中，所有伺服器執行個體和元件都必須是相同版本。 執行最新軟體版本的伺服器會設定伺服陣列中所有伺服器的層級。 如果您只要升級部分伺服器，執行較舊版軟體的伺服器在升級之前將變成無法使用。  
  
 升級第一部伺服器之後，尚未升級的其他伺服器 **將會變成無法使用**。 在所有伺服器執行相同層級之後，即可恢復使用。  
  
 SQL Server 安裝程式會就地升級實體電腦上的 PowerPivot 方案檔案，但是若要升級伺服器陣列使用的方案，則必須使用本主題前面章節中所描述的 PowerPivot 組態工具。  
  
 
  
##  <a name="qfe"></a> 將 QFE 套用至伺服器陣列中的 PowerPivot 執行個體  
 修補 PowerPivot for SharePoint 伺服器會將現有的程式檔案更新成包含特定問題修正的較新版本。 將 QFE 套用至多重伺服器拓撲時，沒有您必須先開始的主要伺服器。 只要您將相同的 QFE 套用至伺服陣列中的其他 PowerPivot 伺服器，就可以從任何伺服器開始。  
  
 套用 QFE 時，您也必須在伺服器陣列組態資料庫中執行更新伺服器版本資訊的組態設定。 已修補之伺服器的版本會變成預期的伺服陣列新版本。 在所有機器上套用並設定 QFE 之前，沒有 QFE 的 PowerPivot for SharePoint 執行個體將無法用於處理 PowerPivot 資料的要求。  
  
 為確保正確套用並設定 QFE，請遵循下列指示進行：  
  
1.  使用隨附在 QFE 中的指示，安裝修補程式。  
  
2.  啟動 PowerPivot 組態工具。  
  
3.  按一下 **[升級功能、服務、應用程式和方案]**，然後按一下 **[確定]**。  
  
4.  檢閱升級工作中所包含的動作，然後按一下 **[驗證]**。  
  
5.  按一下 **[執行]** 套用動作。  
  
6.  針對伺服器陣列中的其他 PowerPivot for SharePoint 執行個體，重複這個動作。  
  
    > [!IMPORTANT]  
    >  在多重伺服器部署中，請務必先修補並設定每個執行個體，然後再繼續進行下一部機器。 PowerPivot 組態工具必須先完成目前執行個體的升級工作，才能移到下一個執行個體。  
  
 若要檢查伺服器陣列中服務的版本資訊，請在管理中心中的 [升級與修補管理] 區段中，使用 **[檢查產品與修補程式安裝狀態]** 頁面。  
  
##  <a name="verify"></a> 升級後的驗證工作  
 升級完成後，使用下列步驟來驗證伺服器正常運作。  
  
|工作|連結|  
|----------|----------|  
|確認伺服器在執行 PowerPivot for SharePoint 的所有電腦上執行。|[啟動或停止 PowerPivot for SharePoint 伺服器](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)|  
|確認網站集合層級的功能啟用。|[為在 [管理中心] 的 [網站集合啟用 PowerPivot 功能整合](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|  
|確認個別的 PowerPivot 活頁簿會透過開啟活頁簿，並按一下篩選與交叉分析篩選器起始查詢來正確載入。|檢查快取的檔案是否存在硬碟上。 快取的檔案可確認資料檔案已在實體伺服器上載入。 尋找 c:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\Backup 資料夾中的快取檔案。|  
|在設定為資料重新整理的所選活頁簿上測試資料重新整理。|測試資料重新整理最簡單的方式就是修改資料重新整理排程，也就是選擇 **[並且盡快重新整理]** 核取方塊，讓資料重新整理立即執行。 此步驟將判斷目前活頁簿的資料重新整理是否成功。 針對其他常用的活頁簿重複這些步驟以確保資料重新整理運作正常。 如需有關排程資料重新整理，請參閱 <<c0> [ 排程資料重新整理&#40;PowerPivot for SharePoint&#41;](../../../2014/analysis-services/schedule-a-data-refresh-powerpivot-for-sharepoint.md)。</c0>|  
|一段時間之後，監視 PowerPivot 管理儀表板中的資料重新整理報表以確認沒有資料重新整理錯誤。|[PowerPivot 管理儀表板和使用量資料](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)|  
  
 如需如何設定 PowerPivot 設定與功能的詳細資訊，請參閱[管理中心的 PowerPivot 伺服器管理和組態](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)。  
  
 引導您完成所有安裝後組態工作的逐步指示，請參閱[初始設定&#40;PowerPivot for SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)。  
  

  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 各版本所支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
