---
title: "儲存封裝 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.savecopyas.f1"
helpviewer_keywords: 
  - "Integration Services 封裝, 儲存"
  - "封裝 [Integration Services], 儲存"
  - "儲存封裝"
  - "SSIS 封裝, 儲存"
  - "SQL Server Integration Services 封裝, 儲存"
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
caps.latest.revision: 48
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 47
---
# 儲存封裝
  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，您可以使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師來建立封裝，並將封裝儲存為檔案系統中的 XML 檔案 (.dtsx 檔案)。 您也可以將封裝 XML 檔案的複本儲存至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 msdb 資料庫，或儲存至封裝存放區。 封裝存放區代表 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務所管理之檔案系統位置中的資料夾。  
  
 如果您將封裝儲存至檔案系統，可以在稍後使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務將封裝匯入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或匯入封裝存放區。 如需詳細資訊，請參閱[匯入和匯出封裝 &#40;SSIS 服務&#41;](../integration-services/service/import-and-export-packages-ssis-service.md)。  
  
 您也可以使用命令提示字元公用程式 **dtutil**，在檔案系統與 msdb 之間複製封裝。 如需詳細資訊，請參閱 [dtutil Utility](../integration-services/dtutil-utility.md)。  
  
### 若要儲存封裝  
  
-   [將封裝儲存至檔案系統](../Topic/Save%20a%20Package%20to%20the%20File%20System.md)  
  
-   [儲存封裝的複本](../Topic/Save%20a%20Copy%20of%20a%20Package.md)  
  
  