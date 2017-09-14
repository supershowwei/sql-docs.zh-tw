---
title: "（報表產生器及 SSRS） 為數列指定圖表區域 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10157"
- sql13.rtp.rptdesigner.chartareaproperties.alignment.f1
ms.assetid: dc3c365b-c263-402a-bf6f-c2a7081db073
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d88358516e05214b230ec57b6243168ef9aac048
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="specify-a-chart-area-for-a-series-report-builder-and-ssrs"></a>為數列指定圖表區域 (報表產生器及 SSRS)
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，圖表是最上層的容器，其中包含外框、圖表標題和圖例。 根據預設，圖表會包含一個*圖表區域*。 在圖表介面上看不到圖表區域，但是您可以將圖表區域視為僅包含軸標籤、軸標題，以及一或多個數列之繪圖區的容器。 下圖顯示單一圖表內多個圖表區域的概念。  
  
 ![顯示一個圖表區域的圖](../../reporting-services/report-design/media/chartareasdiagram.gif "顯示一個圖表區域的圖")  
  
 依預設，所有數列都會加入到預設的圖表區域中。 使用區域圖、直條圖、折線圖和散佈圖時，這些數列的任何組合都可以顯示在相同的圖表區域中。 如果您在相同的圖表區域中有數個數列，則會降低圖表的可讀性。 您可能想要將圖表類型分為數個圖表區域。 使用多個圖表區域將會增加可讀性，讓比較更為容易。 例如，價格-數量股票圖通常有不同範圍的值，但是可以在相同一段時間的價格和數量資料之間進行比較。  
  
 長條圖、極座標圖或形狀圖數列僅能與相同圖表區域中相同圖表類型的數列結合。 如果您使用的是極座標圖或形狀圖，請考慮將個別的圖表資料區域用於您要顯示的每個欄位。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-associate-a-series-with-a-new-chart-area"></a>讓數列與新圖表區域產生關聯  
  
1.  以滑鼠右鍵按一下圖表的任何位置，然後選取 [加入新的圖表區域]。 新的空白圖表區域就會出現在圖表上。  
  
2.  以滑鼠右鍵按一下圖表上的數列，或者在 [圖表資料] 窗格以滑鼠右鍵按一下適當區域中的資料欄位，然後按一下 [數列屬性]。  
  
3.  在 **[軸和圖表區域]**中，選取您要數列顯示在其中的圖表區域。  
  
4.  (選擇性) 垂直對齊圖表區域。 若要這樣做，以滑鼠右鍵按一下圖表，然後選取 [圖表區域屬性]。 在 **[對齊]**中，選取您要與所選圖表區域對齊的另一個圖表區域。  
  
## <a name="see-also"></a>請參閱＜  
 [圖表 &#40; 上的多個數列報表產生器及 SSRS &#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表 &#40; 上的資料點報表產生器及 SSRS &#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [使用調色盤 &#40; 圖表上定義色彩報表產生器及 SSRS &#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [極座標圖 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)   
 [形狀圖 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [圓形圖 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  