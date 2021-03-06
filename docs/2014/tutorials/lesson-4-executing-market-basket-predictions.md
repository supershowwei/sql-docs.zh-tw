---
title: 第 4 課：執行購物籃預測 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b3238f1b-ea04-4253-ade2-838a806b62fe
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3b49fc242eb8b2242269c5af33cc094937bbe0de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312104"
---
# <a name="lesson-4-executing-market-basket-predictions"></a>第 4 課：執行購物籃預測
  在這一課，您將使用 DMX`SELECT`陳述式來建立預測，根據關聯模型中建立[第 2 課：將採礦模型加入購物籃採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)。 預測查詢的建立方式是使用 DMX `SELECT` 陳述式並加入 `PREDICTION JOIN` 子句。 在預測聯結之語法的詳細資訊，請參閱[FROM&#60;模型&#62;預測聯結&#40;DMX&#41;](/sql/dmx/select-from-model-cases-dmx)。  
  
 **SELECT FROM\<模型 > PREDICTION JOIN**形式的`SELECT`陳述式包含三個部分：  
  
-   結果集傳回的採礦模型資料行和預測函數的清單。 這份清單也可以包含來源資料的輸入資料行。  
  
-   定義用來建立預測之資料的來源查詢。 例如，如果您要在單一批次中建立許多預測，來源查詢就可以擷取客戶的清單。  
  
-   採礦模型資料行和來源資料之間的對應。 如果資料行名稱相符，您就可以使用 `NATURAL PREDICTION JOIN` 語法並省略資料行對應。  
  
 您可以使用預測函數來強化查詢。 預測函數會提供其他資訊，例如發生預測的機率，或提供對定型資料集的預測支援。 如需有關預測函數的詳細資訊，請參閱[函式&#40;DMX&#41;](/sql/dmx/functions-dmx)。  
  
 您也可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中使用預測查詢產生器來建立預測查詢。  
  
## <a name="singleton-prediction-join-statement"></a>單一 PREDICTION JOIN 陳述式  
 第一個步驟是建立單一查詢中，使用**SELECT FROM\<模型 > PREDICTION JOIN**語法並提供一組值做為輸入。 以下是單一陳述式的一般範例：  
  
```  
SELECT <select list>  
    FROM [<mining model>]   
[NATURAL] PREDICTION JOIN  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
AS [<input alias>]  
```  
  
 第一行程式碼會定義在採礦模型中由查詢傳回的資料行，並且指定用來產生預測之採礦模型的名稱：  
  
```  
SELECT <select list> FROM [<mining model>]   
```  
  
 下一行程式碼會指出要執行的作業。 由於您將針對每個資料行指定值並輸入與模型完全相符的資料行名稱，因此可以使用 `NATURAL PREDICTION JOIN` 語法。 但是，如果資料行名稱不同，您就必須加入 `ON` 子句來指定此模型中的資料行以及新資料中的資料行之間的對應。  
  
```  
[NATURAL] PREDICTION JOIN  
```  
  
 接下來幾行的程式碼定義購物車中的產品，它們將用來預測客戶可能加入的其他產品：  
  
```  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
```  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   建立一個查詢，而此查詢會依據客戶購物車中已有的項目來預測客戶可能購買的其他項目。 您將建立此查詢使用採礦模型的預設值*MINIMUM_PROBABILITY*。  
  
-   建立一個查詢，而此查詢會依據客戶購物車中已有的項目來預測客戶可能購買的其他項目。 此查詢根據不同的模型，當中*MINIMUM_PROBABILITY*已設定為 0.01。 因為預設值*MINIMUM_PROBABILITY*關聯模型中為 0.3，此模型上的查詢應傳回比查詢更可能的項目上的預設模型。  
  
## <a name="create-a-prediction-by-using-a-model-with-the-default-minimumprobability"></a>使用具有預設 MINIMUM_PROBABILITY 的模型建立預測  
  
#### <a name="to-create-an-association-query"></a>若要建立關聯查詢  
  
1.  在**物件總管] 中**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**以開啟 [查詢編輯器。  
  
2.  將 `PREDICTION JOIN` 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <select list>   
    ```  
  
     成為：  
  
    ```  
    PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
     您可以只包含資料行名稱 [Products]，但使用[Predict &#40;DMX&#41; ](/sql/dmx/predict-dmx)函式，您可以限制為三個演算法所傳回的產品數目。 您也可以使用 `INCLUDE_STATISTICS`，它可傳回每一項產品的支援、機率和調整機率。 這些統計資料有助您評比預測的精確性。  
  
4.  取代下列項目：  
  
    ```  
    [<mining model>]   
    ```  
  
     成為：  
  
    ```  
    [Default Association]  
    ```  
  
5.  取代下列項目：  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     成為：  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     此陳述式會使用 `UNION` 陳述式來指定三項產品，而這些產品必須連同預測的產品一起加入購物車內。 `SELECT` 陳述式中的 Model 資料行會對應到巢狀產品資料表所包含的模型資料行。  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT  
      PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Default Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
7.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Association Prediction.dmx`。  
  
8.  在工具列上，按一下**Execute**  按鈕。  
  
     查詢會傳回包含三項產品的資料表：HL Mountain Tire、 Fender Set-Mountain 和 ML Mountain Tire。 此資料表會按照機率的順序列出這些傳回的產品。 最有可能與查詢中指定之三項產品加入同一個購物車的傳回產品會顯示在資料表的最上方。 後面兩項產品則是後續最有可能加入購物車的產品。 此資料表也包含描述預測精確性的統計資料。  
  
## <a name="create-a-prediction-by-using-a-model-with-a-minimumprobability-of-001"></a>使用具有 MINIMUM_PROBABILITY 0.01 的模型建立預測  
  
#### <a name="to-create-an-association-query"></a>若要建立關聯查詢  
  
1.  在**物件總管] 中**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**以開啟 [查詢編輯器。  
  
2.  將 `PREDICTION JOIN` 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <select list>   
    ```  
  
     成為：  
  
    ```  
    PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
4.  取代下列項目：  
  
    ```  
    [<mining model>]   
    ```  
  
     成為：  
  
    ```  
    [Modified Association]  
    ```  
  
5.  取代下列項目：  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     成為：  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     此陳述式會使用 `UNION` 陳述式來指定三項產品，而這些產品必須連同預測的產品一起加入購物車內。 `SELECT` 陳述式中的 `[Model]` 資料行會對應到巢狀產品資料表中的資料行。  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT  
      PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Modified Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
7.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Modified Association Prediction.dmx`。  
  
8.  在工具列上，按一下**Execute**  按鈕。  
  
     查詢會傳回包含三項產品的資料表：HL Mountain Tire、 Water Bottle 和 Fender Set-Mountain。 此資料表會按照機率的順序列出這些產品。 顯示在資料表最上方的產品就是最有可能與查詢中指定之三項產品加入同一個購物車的產品。 其餘產品則是後續最有可能加入購物車的產品。 此資料表也包含描述預測精確度的統計資料。  
  
     您可以看到查詢，這個結果的值*MINIMUM_PROBABILITY*參數會影響查詢所傳回的結果。  
  
 這是購物籃教學課程的最後步驟。 現在您擁有了一組模型，可用來預測客戶可能會同時購買的產品。  
  
 若要了解如何在另一個預測狀況中使用 DMX，請參閱[Bike Buyer DMX 教學課程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)。  
  
## <a name="see-also"></a>另請參閱  
 [關聯模型查詢範例](../../2014/analysis-services/data-mining/association-model-query-examples.md)   
 [資料採礦查詢介面](../../2014/analysis-services/data-mining/data-mining-query-tools.md)  
  
  
