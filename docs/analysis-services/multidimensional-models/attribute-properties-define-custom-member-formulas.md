---
title: 定義自訂成員公式 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cfeee065f99a9071f7175d8344f7e6eae84a7bc6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62666582"
---
# <a name="attribute-properties---define-custom-member-formulas"></a>屬性內容 - 定義自訂成員公式
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以定義多維度運算式 (MDX) 運算式 (稱為自訂成員公式)，來提供所指定屬性之成員的值。 來自資料來源檢視之資料表中的資料行，為屬性的每一個成員提供該運算式，來提供該成員的值。  
  
 自訂成員公式決定與成員相關聯的資料格值，並覆寫量值的彙總函式。 自訂成員公式是用 MDX 撰寫。 每個自訂成員公式適用於單一成員。 自訂成員公式會儲存在維度資料表中，或者儲存在與維度資料表有外部索引鍵關聯性的另一個資料表中。  
  
 屬性 (Attribute) 上的 **CustomRollupColumn** 屬性 (Property) 指定含有屬性 (Attribute) 成員之自訂成員公式的資料行。 如果資料行中的資料列是空的，則會正常傳回成員的資料格值。 如果資料行中的公式無效，則只要擷取使用成員的資料格值時，就會發生執行階段錯誤。  
  
 在為屬性指定自訂成員公式之前，請確認包含該屬性的維度資料表，或直接相關的資料表中有字串資料行可儲存自訂成員公式。 如果狀況如此的話，您可手動在屬性上設定 **CustomRollupColumn** 屬性，或使用商業智慧精靈的設定自訂成員公式增強功能，在屬性上啟用自訂成員公式。 如需如何使用這項增強功能的詳細資訊，請參閱 [在維度中設定屬性的自訂成員公式](../../analysis-services/multidimensional-models/bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)。  
  
## <a name="evaluating-custom-member-formulas"></a>評估自訂成員公式  
 自訂成員公式與導出成員不同。 自訂成員公式是套用至維度資料表中的成員，並只提供成員的值。 相反地，導出成員不是儲存在維度資料表中，而導出成員運算式會定義維度或階層所含之其他成員的資料和中繼資料。  
  
 自訂成員公式覆寫與量值相關聯的彙總函式。 例如，在指定自訂成員公式之前，使用 **Sum** 彙總函式的量值含有 Time 維度下列成員的下列值：  
  
-   2003:2100  
  
    -   第 1 季：700  
  
    -   季 2:500  
  
    -   季 3:100  
  
    -   Quarter 4:800  
  
-   2004:1500  
  
    -   第 1 季：600  
  
    -   季 2:200  
  
    -   季 3:300  
  
    -   Quarter 4:400  
  
 利用自訂成員公式，成員的值將改由自訂積存公式提供。 例如，可使用以下自訂成員公式，提供 Time 維度之 2004 成員 Quarter 4 子成員的值 450。  
  
```  
Time.[Quarter 3] * 1.5  
```  
  
 自訂成員公式儲存在維度資料表的一個資料行中。 您可以在屬性上設定 **CustomRollupColumn** 屬性，來啟用自訂積存公式。  
  
 若要將單一 MDX 運算式套用至屬性的所有成員，請在維度資料表上建立具名計算，以常值字串傳回 MDX 運算式。 然後，以您要設定之屬性上的 **CustomRollupColumn** 屬性設定，來指定具名計算。 具名計算是資料來源檢視資料表中的一個資料行，它傳回 SQL 運算式所定義的資料列值。 如需建構具名計算的詳細資訊，請參閱[在資料來源檢視中定義具名計算 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
> [!NOTE]  
>  若要將 MDX 運算式套用至特定層級的成員，而非以特定屬性為基礎之所有層級的成員，則可將運算式定義為層級上的 MDX 指令碼。 如需詳細資訊，請參閱 [MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)。  
  
 如果您對屬性的成員同時使用導出成員和自訂積存公式，則必須知道評估順序。 導出成員是在解析自訂積存公式之前解析。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [在維度中設定屬性的自訂成員公式](../../analysis-services/multidimensional-models/bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)  
  
  
