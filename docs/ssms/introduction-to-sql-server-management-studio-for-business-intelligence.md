---
title: 適用於 BI 的 SQL Server Management Studio 簡介 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4e928be305f701c8493e03fea504c8d275226966
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215374"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>適用於商業智慧的 SQL Server Management Studio 簡介
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
若要存取、設定及管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)]、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，請使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 雖然這三種商業智慧技術全都依賴 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，但是與每一項技術有關的管理工作則會有些微的差異。  
  
> [!NOTE]
> 若要建立及修改 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 解決方案，請使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)]，而不要使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)] 是一個以 [!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)]為根據的開發環境。  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Analysis Services 解決方案  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可讓您管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 物件，例如執行備份及處理物件。  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 會提供一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 指令碼專案，您可在其中開發及儲存使用多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 和 XML for Analysis (XMLA) 所撰寫的指令碼。 您可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 指令碼專案來執行管理工作或是在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 執行個體上重新建立物件，例如資料庫和 Cube。 例如，您可以在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 指令碼專案中開發 XMLA 指令碼，該指令碼會直接在現有的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 執行個體上建立新的物件。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 指令碼專案可儲存成為方案的一部分，並與原始程式碼控制整合。  
  
如需如何使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的詳細資訊，請參閱 [使用 SQL Server Management Studio 進行開發和實作](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md)。  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Integration Services 解決方案  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可讓您使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務來管理套件及監視執行中的套件。 您也可以使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 將封裝組織成資料夾、執行封裝、匯入及匯出封裝、移轉 Data Transformation Services (DTS) 封裝及升級 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 來管理 Reporting Services 專案  
使用 SQL Server Management Studio 可啟用 Reporting Services 功能、管理服務和資料庫，以及管理角色和作業。  
  
您可使用 [共用排程] 資料夾來管理共用排程，並管理報表伺服器資料庫 (ReportServer、ReportServerTempdb)。 當您將報表伺服器資料庫移到新的或另一個 SQL Server 資料庫引擎 ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)]) 時，您也會在 Master 系統資料庫中建立 RSExecRole。 如需有關這些工作的詳細資訊，請參閱下列主題：  
  
-   [Management Studio 的如何主題](https://msdn.microsoft.com/60685458-9108-47bf-820a-5e7db454d408)  
  
-   [管理報表伺服器資料庫](../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)  
  
-   [如何：建立 RSExecRole](../reporting-services/security/create-the-rsexecrole.md)  
  
您也可以透過以下方式來管理伺服器：啟用及設定各種功能、設定伺服器預設值及管理角色和作業。 如需有關這些工作的詳細資訊，請參閱下列主題：  
  
-   [如何：設定報表伺服器屬性 (Management Studio)](https://msdn.microsoft.com/1ed0f84b-b12a-4e49-b65c-a11a99f9093f)  
  
-   [如何：建立、刪除或修改角色 (Management Studio)](https://msdn.microsoft.com/3d1d56e6-a283-44a7-8417-36cb4d2c74d1)  
  
-   [啟用和停用 Reporting Services 的用戶端列印](https://msdn.microsoft.com/0e709c96-7517-4547-8ef6-5632f8118524)  
  
## <a name="see-also"></a>另請參閱  
[使用 SQL Server Data Tools 進行開發和實作](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
[SQL Server 資料工具中的 Reporting Services](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
