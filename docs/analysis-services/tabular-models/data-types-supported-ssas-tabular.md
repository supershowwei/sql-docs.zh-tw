---
title: Analysis Services 表格式模型中支援的資料型別 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 33618c019e59c044e681c45130130adc79d53122
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472197"
---
# <a name="data-types-supported-in-tabular-models"></a>支援表格式模型中的資料類型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文描述可用於表格式模型中的資料類型，並討論在 Data Analysis Expressions (DAX) 公式中計算或使用資料時，隱含的資料類型轉換。  

  
##  <a name="bkmk_data_types"></a> 表格式模型中使用的資料類型  
當您在公式中匯入資料或使用值時，即使原始資料來源包含不同的資料類型，該資料還是會轉換成下列其中一種資料類型。 由公式所產生的值也會使用這些資料類型。  
  
 一般來說，實作這些資料類型是為了在導出資料行中達成精確的計算，而且相同的限制會套用到模型中的其餘資料上以保持一致性。  
  
 用於數字、貨幣、日期和時間的格式應該遵照用來處理模型資料之用戶端上所指定地區設定的格式。 您可以使用模型中的格式選項來控制顯示值的方式。  
  
||||  
|-|-|-|  
|**模型中的資料類型**|**DAX 中的資料類型**|**說明**|  
|整數|64 位元 (八位元組) 整數值*<br /><br /> 注意:<br />         DAX 公式不支援小到無法容納描述列示之最小值的資料類型。|沒有小數位數的數字。 整數可以是正數或負數，但必須是 -9,223,372,036,854,775,808 (-2^63) 到 9,223,372,036,854,775,807 (2^63-1) 之間的整數。|  
|十進位數字|64 位元 (八位元組) 實數*<br /><br /> 注意:<br />         DAX 公式不支援小到無法容納描述列示之最小值的資料類型。|實數是可以有小數位數的數字。 實數涵蓋極廣的值範圍：<br /><br /> 負值是從 -1.79E + 308 到 -2.23E - 308<br /><br /> 零 (0)<br /><br /> 正值是從 2.23E -308 到 1.79E + 308<br /><br /> 不過，有效位數的數目限制為 17 個小數位數。|  
|布林|布林|True 或 False 值。|  
|Text|String|Unicode 字元資料字串。 可以是字串、 數字或以文字格式表示的日期。|  
|date|日期/時間|採用可接受之日期時間表示方式的日期和時間。<br /><br /> 有效日期為 1900 年 3 月 1 日之後的所有日期。|  
|CURRENCY|CURRENCY|貨幣資料類型允許的值是從 -922,337,203,685,477.5808 到 922,337,203,685,477.5807 且固定有效位數為四個小數位數。|  
|N/A|空白|空白是 DAX 中表示和取代 SQL Null 的資料類型。 您可以使用 BLANK 函數建立空白，然後使用邏輯函數 ISBLANK 來測試空白。|  
  
 \* 如果您嘗試匯入有大數值的資料，匯入可能會失敗，發生下列錯誤：  
  
 記憶體中資料庫錯誤：'\<資料行名稱 >' 的資料行'\<資料表名稱 >' 資料表包含的值 ' 1.7976931348623157 e + 308'，不受支援。 已取消作業。  
  
 這項錯誤發生的原因是，模型設計師使用該值來代表 Null。 下列清單中的值是前述 Null 值的同義字：  
  
||  
|-|  
|值|  
|9223372036854775807|  
|-9223372036854775808|  
|1.7976931348623158e+308|  
|2.2250738585072014e-308|  
  
 移除您的資料中的值，並再試一次匯入。  
  
> [!NOTE]  
>  您不能從字串長度超過 131,072 個字元的 **varchar(max)** 資料行匯入。  
  
### <a name="table-data-type"></a>資料表資料類型  
 此外，DAX 還使用 *「資料表」* (Table) 資料類型。 DAX 會在許多函數中使用這個資料類型，例如彙總與時間智慧計算。 有些函數需要使用資料表的參考；有些函數則會傳回之後可當做其他函數輸入使用的資料表。 在需要資料表當做輸入的部分函數中，您可以指定評估為資料表的運算式；對於某些函數，則需要基底資料表的參考。 如需特定函數需求的相關資訊，請參閱 [DAX 函數參考](http://msdn.microsoft.com/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b)。  
  
##  <a name="bkmk_implicit"></a> DAX 公式中隱含與明確的資料類型轉換
  
 每個 DAX 函數對於當做輸入與輸出使用之資料的類型都有特定需求。 例如，某些函數需要整數做為部分引數並需要日期做為其他引數；其他函數則需要文字或資料表。  
  
 如果您指定的引數的資料行中的資料與函數所需的資料類型不相容，DAX 在許多情況下會傳回錯誤。 不過，只要可能的話，DAX 會嘗試隱含資料轉換成所需的資料類型。 例如：  
  
-   您可以輸入一個數字，例如"123"，做為字串。 DAX 剖析字串，並嘗試將指定為數字的資料類型。  
  
-   您可以加入 TRUE + 1 然後得到結果 2，因為 TRUE 會隱含地轉換為數字 1 並執行 1+1 的運算。  
  
-   如果您在兩個資料行中加入值，且其中一個值恰巧表示為文字 ("12")，而另一個值表示為數字 (12)，DAX 就會將字串隱含地轉換為數字，然後執行加法以得到數值結果。 下列運算式會傳回 44：= "22" + 22  
  
-   如果您嘗試串連兩個數字，它們會顯示為字串，並再串連。 下列運算式會傳回 "1234"：= 12 & 34  
  
 下表摘要說明在公式中執行的隱含資料類型轉換。 一般而言，語意模型設計師的行為類似 Microsoft Excel，當指定的運算需要時，就會盡可能執行隱含的轉換。  
  
### <a name="table-of-implicit-data-conversions"></a>隱含資料轉換的資料表  
 所執行的轉換類型取決於運算子，運算子會在執行要求的運算前，轉換所需的值。 這些資料表會列出運算子，並在資料類型與相交之資料列的資料類型配對時，指出針對資料行中的每個資料類型所執行的轉換。  
  
> [!NOTE]  
>  文字資料類型不包含在這些資料表中。 當數字以文字格式，在某些情況下，表示時模型設計工具會嘗試判斷數字類型，並以數字表示該。  
  
#### <a name="addition-"></a>加 (+)  
  
||||||  
|-|-|-|-|-|  
|運算子 (+)|INTEGER|貨幣|real|日期/時間|  
|INTEGER|INTEGER|貨幣|real|日期/時間|  
|CURRENCY|CURRENCY|CURRENCY|real|日期/時間|  
|real|real|real|real|日期/時間|  
|日期/時間|日期/時間|日期/時間|日期/時間|日期/時間|  
  
 例如，如果在加法運算中使用實數搭配貨幣資料，兩個值都會轉換為 REAL，因此傳回的結果為 REAL。  
  
#### <a name="subtraction--"></a>減 (-)  
 在下表中，資料列標頭是被減數 （左側），資料行標頭則是減數 （右側）：  
  
||||||  
|-|-|-|-|-|  
|運算子 (-)|INTEGER|貨幣|real|日期/時間|  
|INTEGER|INTEGER|貨幣|real|real|  
|CURRENCY|CURRENCY|CURRENCY|real|real|  
|real|real|real|real|real|  
|日期/時間|日期/時間|日期/時間|日期/時間|日期/時間|  
  
 例如，如果在減法運算中使用日期搭配其他任何資料類型，兩個值都會轉換為日期，因此傳回值也是日期。  
  
> [!NOTE]  
>  表格式模型也支援一元運算子 - (否定)，但是這個運算子不會變更運算元的資料類型。  
  
#### <a name="multiplication-"></a>乘 (*)  
  
||||||  
|-|-|-|-|-|  
|運算子 (*)|INTEGER|貨幣|real|日期/時間|  
|INTEGER|INTEGER|貨幣|real|INTEGER|  
|CURRENCY|CURRENCY|real|CURRENCY|CURRENCY|  
|real|real|CURRENCY|real|real|  
  
 例如，如果在乘法運算中結合整數與實數，兩個值都會轉換為實數，因此傳回值也是 REAL。  
  
#### <a name="division-"></a>除 (/)  
 在下表中，資料列標頭是被除數 (分子)，而資料行標頭則是除數 (分母)。  
  
||||||  
|-|-|-|-|-|  
|運算子 (/)<br /><br /> (資料列/資料行)|INTEGER|貨幣|real|日期/時間|  
|INTEGER|real|CURRENCY|real|real|  
|CURRENCY|CURRENCY|real|CURRENCY|real|  
|real|real|real|real|real|  
|日期/時間|real|real|real|real|  
  
 例如，如果在除法運算中結合整數與貨幣值，兩個值都會轉換為實數，因此結果也是實數。  
  
#### <a name="comparison-operators"></a>比較運算子  
支援僅提供有限的混合的資料類型的比較作業的組合。 若要深入了解，請參閱 [DAX 運算子參考](https://msdn.microsoft.com/library/ee634237.aspx)。  
  
## <a name="bkmk_hand_blanks"></a> 空白、 空字串與零值的處理  
 下表摘要說明 DAX 與差異在 Microsoft Excel 中的空白處理方式：  
  
||||  
|-|-|-|  
|運算式|DAX|[匯出]|  
|BLANK + BLANK|BLANK|0 (零)|  
|BLANK +5|5|5|  
|BLANK * 5|BLANK|0 (零)|  
|5/BLANK|無限|錯誤|  
|0/BLANK|NaN|錯誤|  
|BLANK/BLANK|空白|錯誤|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|BLANK|錯誤|  
|BLANK AND BLANK|BLANK|錯誤|  
  
 如需特定函數或運算子如何處理空白的詳細資訊，請參閱 [DAX 函數參考](http://msdn.microsoft.com/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b)一節中，每個 DAX 函數的個別主題。  
  
