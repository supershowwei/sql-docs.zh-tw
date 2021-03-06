---
title: 第 4 課：以程式設計方式更新報表定義 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1f0a1d46-6d6d-4f67-b51e-06dbbbffacf9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 703643f2c51ec86090cb03ba7089080dfe416620
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63137459"
---
# <a name="lesson-4-update-the-report-definition-programmatically"></a>第 4 課：以程式設計方式更新報表定義
  既然已經使用報表欄位從報表伺服器載入報表定義，並且您具有對它的參考，就必須更新報表定義。 在此範例中，您將更新報表的 `Description` 屬性。  
  
### <a name="to-update-the-report-definition"></a>更新報表定義  
  
1.  取代 UpdateReportDefinition() 方法，在 Program.cs 檔案中的程式碼 (如 Module1.vb [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 為下列程式碼：  
  
    ```csharp  
    private void UpdateReportDefinition()  
    {  
        System.Console.WriteLine("Updating Report Definition");  
  
        // Create a list of the Items Choices for the Report. The   
        // ItemsChoiceType118 enum represents all the properties  
        // available in the report and the ItemsElementName   
        // represents the properties that exist in the current   
        // instance of the report.  
        List<ItemsChoiceType118> _reportItems =   
            new List<ItemsChoiceType118>(_report.ItemsElementName);  
  
        // Locate the index for the Description property  
        int index = _reportItems.IndexOf(  
            ItemsChoiceType118.Description);  
  
        // The Description item is of type StringLocIDType, so   
        // cast the item type first and then assign new value.  
        System.Console.WriteLine("- Old Description: " +   
            ((StringLocIDType)_report.Items[index]).Value );  
  
        // Update the Description for the Report  
        ((StringLocIDType)_report.Items[index]).Value =   
            "New Report Description";  
  
        System.Console.WriteLine("- New Description: " +   
            ((StringLocIDType)_report.Items[index]).Value );  
    }  
    ```  
  
    ```vb  
    Private Sub UpdateReportDefinition()  
  
        System.Console.WriteLine("Updating Report Definition")  
  
        'Create a list of the Items Choices for the Report. The   
        'ItemsChoiceType118 enum represents all the properties  
        'available in the report and the ItemsElementName   
        'represents the properties that exist in the current   
        'instance of the report.  
        Dim reportItems As List(Of ItemsChoiceType118) = _  
            New List(Of ItemsChoiceType118)(m_report.ItemsElementName)  
  
        'Locate the index for the Description property  
        Dim index As Integer = _  
            reportItems.IndexOf(ItemsChoiceType118.Description)  
  
        'The Description item is of type StringLocIDType, so   
        'cast the item type first and then assign new value.  
        System.Console.WriteLine("- Old Description: " & _  
            DirectCast(m_report.Items(index), StringLocIDType).Value)  
  
        'Update the Description for the Report  
        DirectCast(m_report.Items(index), StringLocIDType).Value = _  
            "New Report Description"  
  
        System.Console.WriteLine("- New Description: " & _  
            DirectCast(m_report.Items(index), StringLocIDType).Value)  
  
    End Sub  
    ```  
  
## <a name="next-lesson"></a>下一課  
 在下一課中，會將已更新的報表定義存回報表伺服器上。 請參閱[第 5 課：將報表定義發行到報表伺服器](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用從 RDL 結構描述產生的類別更新報表&#40;SSRS 教學課程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)  
  
  
