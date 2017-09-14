---
title: "ODBC 連接管理員 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.odbcconnection.f1
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: f3e331efe9c6a297ef8d9dc342fb07c83ddafc03
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="odbc-connection-manager"></a>ODBC 連接管理員
  ODBC 連接管理員可使用「開放式資料庫連接 (ODBC)」規格，讓封裝連接到各種資料庫管理系統。  
  
 當您將 ODBC 連接加入封裝並設定連線管理員屬性時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立連線管理員，並將該連線管理員加入到封裝的 **Connections** 集合。 在執行階段，連接管理員會解析為實體 ODBC 連接。  
  
 連線管理員的 **ConnectionManagerType** 屬性會設為 **ODBC**。  
  
 您可以利用下列方式設定 ODBC 連接管理員：  
  
-   提供參考使用者或系統資料來源名稱的連接字串。  
  
-   指定要連接的伺服器。  
  
-   指示在執行階段是否保留連接。  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>設定 ODBC 連接管理員  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [ODBC 連接管理員 UI 參考](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)  
  
 如需以程式設計方式設定連線管理員的相關資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="odbc-connection-manager-ui-reference"></a>ODBC 連接管理員 UI 參考
  使用 **[設定 ODBC 連接管理員]** 對話方塊，將連接加入 ODBC 資料來源。  
  
 若要深入了解 ODBC 連接管理員，請參閱＜ [ODBC Connection Manager](../../integration-services/connection-manager/odbc-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **資料連接**  
 從清單中選取現有的 ODBC 連接管理員。  
  
 **資料連接屬性**  
 檢視選取之 ODBC 連接管理員的屬性與值。  
  
 **新增**  
 使用 [連線管理員] 對話方塊來建立 ODBC 連線管理員。 此對話方塊也可以讓您在必要時建立新的 ODBC 資料來源。  
  
 **Delete**  
 請選取一個連接，然後使用 [刪除] 按鈕刪除它。  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  