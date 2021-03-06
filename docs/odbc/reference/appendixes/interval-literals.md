---
title: 間隔常值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval literals [ODBC]
- interval data type [ODBC], literals
ms.assetid: f9e6c3c7-4f98-483f-89d8-ebc5680f021b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc5d09bca83724bb956d39512c51c3dc47db1bad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188813"
---
# <a name="interval-literals"></a>間隔常值
ODBC 會需要的所有驅動程式支援 SQL_CHAR 或 SQL_VARCHAR 資料類型的所有 C 間隔資料類型的轉換。 如果基礎資料來源不支援間隔資料類型，不過，此驅動程式必須知道 SQL_CHAR 欄位中的值正確格式，為了支援這些轉換。 同樣地，ODBC 會需要應該有任何的 ODBC C 類型可轉換成 SQL_CHAR 或 SQL_VARCHAR，讓驅動程式必須知道何種格式儲存在字元欄位中的時間間隔。 本章節描述間隔常值，要用來驗證 SQL_CHAR 欄位，或從 C 間隔資料類型的轉換期間所需的驅動程式寫入器的語法。  
  
> [!NOTE]  
>  間隔常值的完整 backus-naur form，BNF 語法如下一節[間隔常值語法](../../../odbc/reference/appendixes/interval-literal-syntax.md)附錄 c:SQL 文法。  
  
 若要將間隔常值傳遞做為 SQL 陳述式的一部分，逸出子句語法定義間隔常值。 如需詳細資訊，請參閱 <<c0> [ 日期、 時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 間隔常值的格式為：  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 其中 「 間隔 」 表示字元常值是間隔。 符號可以是加號或減號;它超出間隔的字串是選擇性的。  
  
 間隔限定詞可以是單一的日期時間欄位也可以包含兩個日期時間欄位，格式： \<*開頭的欄位*> TO \<*尾端欄位*>。  
  
-   當間隔所組成的單一欄位中時，單一欄位可以是可能會伴隨選擇性的開頭有效位數，括號括住的非第二個欄位。 單一的日期時間欄位也可以是另一個欄位，可能會伴隨選擇性的開頭有效位數、 括號中的選擇性小數秒有效位數或兩者。 如果開頭的有效位數與小數秒數有效位數的秒數欄位，會以逗號分隔。 如果秒欄位具有小數秒數有效位數，這時也必須領先的有效位數。  
  
-   間隔由前置和尾端的欄位所組成，開頭的欄位時，可能會伴隨開頭括號括住的欄位有效位數的時間間隔的非第二個欄位。 非第二個欄位或可能伴隨著括號括住間隔小數秒數有效位數的第二個欄位，可以是後端的欄位。  
  
 中的時間間隔字串*值*括在單引號中。 它可以是年-月常值或日期時間常值。 在字串的格式*值*取決於下列規則：  
  
-   此字串包含所默許的每個欄位的十進位值\<*間隔**限定詞*>。  
  
-   如果間隔有效位數包含年份和月份的欄位，這些欄位的值是會以負號分隔。  
  
-   如果間隔有效位數包含日期和小時欄位，這些欄位的值會以空格分隔。  
  
-   如果間隔有效位數會包含 [小時] 欄位和較低的順序欄位 （分鐘與秒），這些欄位的值會以分隔。  
  
-   如果間隔有效位數包含第二個欄位的明示或默示的秒數有效位數為非零值，該字元正前方第一個數字的小數點後的第二個為句點。  
  
-   沒有任何欄位可以是很長，除了兩個以上的數字：  
  
    -   [前置] 欄位的值可以是只要明示或默示間隔開頭有效位數。  
  
    -   第二個欄位的分數部分可以是只要明示或默示的秒數有效位數。  
  
    -   行尾的欄位會依西曆的一般條件約束。 (請參閱[西曆的條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)。)  
  
 下表列出的有效間隔常值間隔的 ODBC 逸出子句中包含的範例。 逸出子句的語法如下所示：  
  
> [!NOTE]  
>  *{間隔登間隔字串間隔限定詞}*  
  
|常值的逸出子句|指定的間隔|  
|---------------------------|------------------------|  
|{INTERVAL '326' YEAR(4)}|指定間隔 326 的年數。 間隔開頭有效位數為 4。|  
|{INTERVAL '326' MONTH(3)}|指定間隔 326 的月數。 間隔開頭有效位數為 3。|  
|{INTERVAL '3261' DAY(4)}|指定間隔 3261 天數。 間隔開頭有效位數為 4。|  
|{INTERVAL '163' HOUR(3)}|指定間隔 163 天數。 間隔開頭有效位數為 3。|  
|{間隔 '163' MINUTE(3)}|指定 163 分鐘的間隔。 間隔開頭有效位數為 3。|  
|{INTERVAL '223.16' SECOND(3,2)}|指定間隔 223.16 的秒數。 間隔開頭有效位數為 3，而秒數有效位數為 2。|  
|{間隔 ' 163-11' 個月的 YEAR(3)}|指定間隔 163 年 11 月數。 間隔開頭有效位數為 3。|  
|{INTERVAL '163 12' DAY(3) TO HOUR}|指定 163 天和 12 小時的間隔。 間隔開頭有效位數為 3。|  
|{INTERVAL '163 12:39' DAY(3) TO MINUTE}|指定 163 天，12 小時 39 分鐘的間隔。 間隔開頭有效位數為 3。|  
|{INTERVAL '163 12:39:59.163' DAY(3) TO SECOND(3)}|指定 163 天，12 小時 39 分鐘的時間，和 59.163 秒的間隔。 間隔開頭有效位數為 3，而且秒數有效位數為 3。|  
|{INTERVAL '163:39' HOUR(3) TO MINUTE}|指定 163 小時 39 分鐘的間隔。 間隔開頭有效位數為 3。|  
|{INTERVAL '163:39:59.163' HOUR(3) TO SECOND(4)}|指定 163 小時、 39 分鐘的時間，以及 59.163 秒的間隔。 間隔開頭有效位數為 3，而且秒數有效位數為 4。|  
|{INTERVAL '163:59.163' MINUTE(3) TO SECOND(5)}|指定 163 分 59.163 秒的間隔。 間隔開頭有效位數為 3，而且秒數有效位數為 5。|  
|{間隔-'16 23:39:56.23' 日至秒鐘}|指定的 16 天，23 小時 39 分鐘的時間，和 56.23 秒減去的間隔。 隱含的開頭有效位數為 2，並隱含的秒數有效位數為 6。|  
  
 下表列出無效的間隔常值的範例：  
  
|常值的逸出子句|原因無效的原因|  
|---------------------------|------------------------|  
|{INTERVAL '163' HOUR(2)}|間隔開頭有效位數為 2，但前置字元欄位的值是 163。|  
|{INTERVAL '223.16' SECOND(2,2)}<br /><br /> {INTERVAL '223.16' SECOND(3,1)}|在第一個範例中，開頭的有效位數為太小，而在第二個範例中，秒數有效位數為太小。|  
|{INTERVAL '223.16' SECOND}<br /><br /> {INTERVAL '223' YEAR}|因為未指定的前置字元的有效位數，它會預設為 2，這是太小無法容納指定的常值。|  
|{INTERVAL '22.1234567' SECOND}|秒數有效位數未指定，因此它會預設為 6。 常值的小數點後具有 7 個位數。|  
|{間隔 ' 163-13' 個月的 YEAR(3)}<br /><br /> {INTERVAL '163 65' DAY(3) TO HOUR}<br /><br /> {INTERVAL '163 62:39' DAY(3) TO MINUTE}<br /><br /> {INTERVAL '163 12:125:59.163' DAY(3) TO SECOND(3)}<br /><br /> {INTERVAL '163:144' HOUR(3) TO MINUTE}<br /><br /> {INTERVAL '163:567:234.163' HOUR(3) TO SECOND(4)}<br /><br /> {間隔 '163:591.163' SECOND(5) 的 MINUTE(3)}|尾端欄位並未遵循西曆的規則。|
