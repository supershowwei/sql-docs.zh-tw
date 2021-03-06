---
title: 定義文字格式 （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00d20f8a6dd4d79b3100549d9286e7534bc8ce6e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240375"
---
# <a name="defining-text-format-text-file-driver"></a>定義文字格式 (文字檔驅動程式)
使用文字驅動程式時，您可以使用**定義文字格式**對話方塊來定義資料行的格式中選取的檔案。 此對話方塊可讓您指定每個資料表的結構描述。 此資訊會寫入到 Schema.ini 檔案資料來源目錄中。 針對每個文字資料來源目錄建立個別的 Schema.ini 檔案。  
  
> [!NOTE]  
>  相同的預設檔案格式適用於所有新的文字資料資料表。 CREATE TABLE 陳述式所建立的所有檔案都繼承這些相同的預設格式值，來選取檔案格式中的值會設定**定義文字格式**對話方塊，其中包含\<預設 >中選擇**資料表**清單。 文字驅動程式不會變更以符合在此對話方塊中，所定義的格式的現有文字檔的格式，但使用的格式，例如它會嘗試從文字檔擷取資料時，會傳回錯誤。  
  
 下列選項位於**定義文字格式** 對話方塊中：  
  
|選項|[資訊]|  
|------------|-----------------|  
|**[加入]**|將使用中的值的資料行**資料型別**，**名稱**，並**寬度**從對話方塊中，且如果適用的話，日期分隔符號值從 Schema.ini。|  
|**字元**|**ANSI**或是**OEM**。 OEM 獌穧非 ANSI 字元集。 如果在選取之項目的格式，這預設為 OEM**資料表**清單尚未先前定義的這個對話方塊。|  
|**資料行名稱的標頭**|指出所選資料表的第一個資料列的資料行是否當做資料行名稱。 任一**真**或是**FALSE**。 預設為 false，因此在選取之項目的格式**資料表**清單尚未先前定義的這個對話方塊。|  
|**資料行**|列出選取的資料表中的每個資料行的資料行名稱。 資料行的順序會反映出資料表中資料行的順序。 如果檔案中已選取，會啟用此清單**資料表**清單。|  
|**資料類型**|可以是位元、 位元組、 CHAR、 貨幣、 日期、 FLOAT、 整數、 LONGCHAR、 SHORT 或單一。 日期資料類型可以是下列格式:"dd-mmm-yy"、"mm-dd-yy"、"mmm-dd-yy"、"-yyyy-mm-dd"或"mmm yyyy-mm-dd"。 "mm"表示數字月份;"mmm"代表月份的字母。|  
|**分隔符號**|指定用來分隔資料行的自訂分隔符號字元。 啟用時機**自訂分隔**選取格式。 此分隔符號可以是只有一個字元、 長度和雙引號 （"） 不能做為分隔符號字元。 （分隔符號不能指定以十六進位或十進位格式）。|  
|**格式**|分隔符號或固定長度。 如果分隔，表示所使用的分隔符號類型： 逗號 (CSV)、 索引標籤上或特殊字元 （自訂）。 此預設值為**CSV 分隔**如果在選取的項目格式**資料表**清單尚未先前定義的這個對話方塊。<br /><br /> 如果**格式**是固定長度和**資料行名稱的標頭**為 TRUE 時，第一行必須是以逗號分隔。|  
|**猜測**|掃描資料表的內容，根據選取的資料表中自動產生的資料行資料類型、 名稱和寬度值的資料行**格式**方塊選取項目。 當資料表格式符號分隔時，就會啟用。 任何先前已定義中的資料行**資料行**清單會被清除並取代為新的項目。 如果**資料行名稱的標頭**是未選取，資料行名稱會自動產生做為 「 F1 」、 「 F2"，等等。 沒有預設值所示**資料型別** 方塊中。<br /><br /> 這項功能只適用於小於 64,513 位元組的資料行。|  
|**修改**|修改使用中的值所選資料行**資料型別**，**名稱**，並**寬度**。|  
|**名稱**|顯示所選取資料行的名稱。 可用來指定現有的資料行或新的資料行的新資料行名稱。<br /><br /> 如果**資料行名稱的標頭**為 TRUE 時，資料行顯示名稱會被忽略。|  
|**移除**|刪除選取的資料行。|  
|**要掃描的資料列**|安裝程式或驅動程式會掃描時設定的資料行和資料行資料類型現有的資料為基礎的資料列數目。<br /><br /> 您可以輸入的數字 1 到 32767 之間之掃描的資料列數目。 此預設值為 25 如果在選取之項目的格式**資料表**清單尚未先前定義的這個對話方塊。 （限制以外的數字會傳回錯誤）。|  
|**資料表**|包含在選取的目錄中的所有檔案的清單**文字安裝**對話方塊中，符合指定的延伸模組的清單。<br /><br /> 當\<預設值 > 選取時，下列其中一項是 true 時，資料表中的屬性值**資料表**Schema.ini (touched Schema.ini 中的沒有其他項目) 寫入群組：<br /><br /> -沒有 Schema.ini 中指定的目錄。<br />-Schema.ini 檔案存在，但沒有區段正在 Schema.ini 的文字檔 （以指定的副檔名） 的目錄中的其中一個。<br />-[文字檔] 區段存在於 Schema.ini，但是主體是空的。<br /><br /> 當\<預設值 > 選取，則**資料行**群組已停用。|  
|**寬度**|CHAR 或 LONGCHAR 資料行可以變更資料行的寬度。 寬度的預設值為 1; 如果在選取之項目的格式**資料表**清單尚未先前定義的這個對話方塊。<br /><br /> 對於其他資料類型，寬度控制項已停用，並會顯示任何值。|
