---
title: 建立採礦模型的複本 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7c5479a43a07a6398ff45635828a2a9c88b7cb11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679463"
---
# <a name="make-a-copy-of-a-mining-model"></a>建立採礦模型的複本
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當您想要快速建立數個以相同資料為基礎的採礦模型時，建立採礦模型的複本很有用。 複製模型之後，可以藉由變更參數或新增篩選來編輯新複本。  
  
 例如，如果您有一個 Customers 資料表與依客戶採購的資料表相連結，則可以建立複本，以針對每個客戶人口統計 (例如年齡或區域等屬性篩選) 建立個別的採礦模型。  
  
 如需如何將模型內容 (如圖形表示形式或模型模式) 複製到剪貼簿以供其他程式使用的資訊，請參閱 [複製採礦模型的檢視](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md)。  
  
### <a name="to-create-a-related-mining-model"></a>若要建立相關的採礦模型  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的方案總管中，按一下包含採礦模型的採礦結構。  
  
2.  按一下 **[採礦模型]** 索引標籤。  
  
3.  選擇模型，然後以滑鼠右鍵按一下，開啟快速鍵功能表。  
  
     -或-  
  
     選取此模型。 在 [採礦模型] 功能表上，選取 [新增採礦模型]。  
  
4.  輸入新採礦模型的名稱，然後選取演算法。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-the-filter-on-the-copied-mining-model"></a>若要編輯複製採礦模型上的篩選  
  
1.  選取採礦模型。  
  
2.  在 [**屬性**] 視窗中，按一下文字方塊，讓**篩選**屬性，然後按一下 [組建 **（...）** ] 按鈕。  
  
3.  變更篩選條件。  
  
     如需如何使用篩選編輯器對話方塊的詳細資訊，請參閱[將篩選套用至採礦模型](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)。  
  
4.  在 [屬性] 視窗的 **AlgorithmParameters** 文字方塊中，按一下 [設定演算法參數]，然後變更演算法參數 (如有必要)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [採礦模型工作和使用說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [從採礦模型刪除篩選](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  
