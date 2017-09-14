---
title: "第 5 課： 設計子報表使用報表精靈 |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 285ade0eaf63fee0733fcfcb9e8f627e8c666a6b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>第 5 課：使用報表精靈設計子報表
在您建立子報表的資料連接和資料表之後，下一步是要使用報表設計師中的 [報表精靈] 設計子報表。 如需有關報表設計工具的詳細資訊，請參閱[使用報表設計工具 &#40; 設計報表SSRS &#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>若要使用報表精靈設計子報表  
  
1.  請確認已在 **方案總管**中選取頂層網站。  
  
2.  以滑鼠右鍵按一下網站，然後選取**加入新項目**。  
  
3.  在**加入新項目**對話方塊中，按一下 **報表精靈**，輸入報表檔的名稱，然後選取**新增**。  
  
    這樣會啟動 [報表精靈]。  
  
4.  在**資料集屬性**頁面上，於**資料來源**方塊中，選取**DataSet2**。  
  
    **可用資料集**方塊會自動更新為您建立的 DataTable。  
  
5.  選取 **[下一步]**。  
  
6.  在**排列欄位**頁面執行下列動作：  
  
    1.  拖曳**ProductID**， **PurchaseOrderID**， **PurchaseOrderDetailID**， **OrderQty**， **ReceivedQty**， **RejectedQty**，和**StockedQty**從**可用的欄位**至**值**方塊。  
  
    2.  選取箭號旁**sum （productid)**， **Sum(PurchaseOrderID)**， **Sum(PurchaseOrderDetailID)**， **Sum(OrderQty)**， **Sum(ReceivedQty)**， **Sum(RejectedQty)**，和**Sum(StockedQty)**清除**總和**選取項目。  
  
7.  選取**下一步**兩次，然後選取**完成**關閉**報表精靈**。  
  
    現在您已建立 .rdlc 檔。 此檔案會在報表設計師中開啟。 您設計的 Tablix 現在會顯示於設計介面中。  
  
8.  在 .rdlc 檔開啟的情況下，執行下列操作加入參數：  
  
    1.  以滑鼠右鍵按一下**參數**中**報表資料**窗格，然後再選取**將參數加入**。  
  
    2.  輸入**productid**中**名稱**方塊。  
  
    3.  確認**整數**中選取**資料型別**清單方塊。  
  
    4.  按一下 **[確定]**。  
  
9. 儲存 .rdlc 檔。  
  
## <a name="next-task"></a>下一項工作  
您已使用 [報表精靈] 成功設計子報表。 接下來您要將 ReportViewer 控制項加入至網站應用程式。 請參閱 [第 6 課：將 ReportViewer 控制項加入至應用程式](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)。  
  
  
  

