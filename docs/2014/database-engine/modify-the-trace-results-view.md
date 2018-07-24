---
title: 修改追蹤結果檢視 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 860a80dc-bac0-4ef0-bf7f-7a9b430d7aa3
caps.latest.revision: 13
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2c1e9c9c2d0041e2e09156e4f33744ea1964812
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302758"
---
# <a name="modify-the-trace-results-view"></a>修改追蹤結果檢視
  本主題描述如何透過執行下列工作，在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中修改擴充事件工作階段的追蹤結果檢視。  
  
1.  [新增或移除資料行](#AddRemoveColumns)  
  
2.  [建立、 編輯或刪除合併的資料行](#ChangeColumns)  
  
3.  [排序結果](#SortResults)  
  
4.  [將結果分組](#GroupResults)  
  
5.  [彙總結果](#AggregateResults)  
  
6.  [篩選結果](#Filter)  
  
7.  [搜尋資料行中的文字](#Search)  
  
8.  [變更顯示設定](#ChangeDisplay)  
  
##  <a name="AddRemoveColumns"></a> 新增或移除資料行  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱，然後選取 **[監看即時資料]**。  
  
2.  在追蹤結果視窗中，以滑鼠右鍵按一下資料行標頭，然後選取 **[選擇資料行]**。  
  
3.  在 **[選擇資料行]** 對話方塊的 **[可用的資料行]** 區段中，選取要新增的資料行名稱，然後按一下向右箭頭。  
  
    > [!NOTE]  
    >  根據預設，資料行依名稱排列。 若要依事件顯示資料行，請按一下 **[依事件排列]**。  
  
     若要移除資料行，請在 **[選取的資料行]** 區段中選取要移除的資料行，然後按一下向左箭頭。  
  
4.  在 **[選取的資料行]** 區段中，若要變更資料行排序顯示，請分別按一下 **[上移]** 或 **[下移]** 。 不能移動多個資料列。  
  
5.  按一下 [確定] 。  
  
##  <a name="ChangeColumns"></a> 建立、 編輯或刪除合併的資料行  
  
#### <a name="to-create-merged-columns"></a>若要建立合併的資料行  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱，然後選取 **[監看即時資料]**。  
  
2.  在追蹤結果視窗中，以滑鼠右鍵按一下資料行標頭，然後按一下 **[選擇資料行]**。  
  
3.  在 **[選擇資料行]** 對話方塊中，按一下 **[新增]**。  
  
4.  在 **[新增合併的資料行]** 對話方塊的 **[合併的資料行名稱]** 方塊中，輸入合併的資料行名稱。  
  
5.  在 **[要合併的原始資料行]** 方塊中，從下拉式清單中選取兩個以上要合併的資料行。  
  
    > [!NOTE]  
    >  擴充事件最多只支援合併五個資料行。  
  
6.  按一下 [確定] 。  
  
#### <a name="to-edit-merged-columns"></a>編輯合併的資料行  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱，然後選取 **[監看即時資料]**。  
  
2.  在追蹤結果視窗中，以滑鼠右鍵按一下資料行標頭，然後按一下 **[選擇資料行]**。  
  
3.  在 **[選擇資料行]** 對話方塊中，按一下 **[編輯]**。  
  
4.  若要變更合併的資料行名稱，請在 **[新增合併的資料行]** 對話方塊的 **[合併的資料行名稱]** 方塊中輸入新名稱。  
  
     若要變更要合併的資料行，請在 **[要合併的原始資料行]** 方塊中，從下拉式清單中選取要合併的資料行，然後按一下 **[確定]**。  
  
#### <a name="to-delete-merged-columns"></a>刪除合併的資料行  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱，然後選取 **[監看即時資料]**。  
  
2.  在追蹤結果視窗中，以滑鼠右鍵按一下資料行標頭，然後按一下 **[選擇資料行]**。  
  
3.  在 **[選擇資料行]** 對話方塊中，選取要刪除之合併資料行的名稱，然後按一下 **[刪除]**。  
  
##  <a name="SortResults"></a> 排序結果  
  
#### <a name="to-sort-the-results-in-ascending-or-descending-order"></a>若要以遞增或遞減順序排序結果  
  
-   開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱、選取 **[監看即時資料]**，然後按一下工具列上的 **[停止資料摘要]** 按鈕。  
  
-   在追蹤結果視窗中，以滑鼠右鍵按一下要排序的資料行標題。 按一下 **[遞增排序]** 或 **[遞減排序]** ，分別以遞增或遞減順序排序資料行。  
  
     如果已對資料行進行分組，則資料行排序只會對群組中的資料進行排序。  
  
##  <a name="GroupResults"></a> 群組結果  
  
#### <a name="to-group-the-results-by-a-single-column"></a>若要依單一資料行將結果分組  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱，選取 **[監看即時資料]**，然後按一下 [擴充事件] 工具列上的 **[停止資料摘要]** 按鈕。  
  
2.  在追蹤結果視窗中，以滑鼠右鍵按一下要分組的資料行標頭，然後按一下 **[依此資料行群組]**。  
  
#### <a name="to-group-the-results-by-multiple-columns"></a>依多個資料行將結果分組  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱、選取 **[監看即時資料]**，然後按一下工具列上的 **[停止資料摘要]** 按鈕。  
  
2.  按一下 [擴充事件] 工具列上的 **[群組]** 按鈕。  
  
3.  在 **[群組]** 對話方塊的 **[可用的資料行]** 方塊中，選取您要分組的資料行，然後按一下向右箭頭。  
  
     若要變更分組順序，請在 **[群組的資料行依據]** 區段中按一下向上箭頭或向下箭頭。  
  
     若要從群組移除資料行，請在 **[群組的資料行依據]** 方塊中選取要移除的資料行，然後按一下向左箭頭。  
  
4.  按一下 [確定] 。  
  
##  <a name="AggregateResults"></a> 彙總結果  
 擴充事件支援五個彙總函式：  
  
-   SUM  
  
-   Min  
  
-   Max  
  
-   平均值  
  
-   Count  
  
 Sum、Min、Max 和 Average 只能搭配可用的數值資料行使用。 Count 是群組中所選資料行的非 Null 值數目。  
  
#### <a name="to-aggregate-results"></a>若要彙總結果  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱、選取 **[監看即時資料]**，然後按一下工具列上的 **[停止資料摘要]** 按鈕。  
  
    > [!NOTE]  
    >  由於彙總是對群組執行，因此您必須先將結果分組，然後才能執行彙總。  
  
2.  在 [擴充事件] 工具列上，按一下 **[彙總]** 按鈕。  
  
     **[彙總]** 對話方塊隨即出現，其中顯示可用於彙總的資料行。  
  
3.  在 **[彙總類型]** 下，從下拉式清單中選取彙總對應資料行的方式。  
  
4.  在 **[彙總排序依據]** 方塊中，從下拉式清單中選取排序依據的資料行。  
  
5.  選取 **[以遞增順序]** 選項，依遞增順序來排序彙總結果。  
  
6.  選取 **[以遞減順序]** 選項，依遞減順序來排序彙總結果。  
  
7.  按一下 [確定] 。  
  
##  <a name="Filter"></a> 篩選結果  
 您可以套用篩選以縮小追蹤視窗中顯示的追蹤結果範圍。 顯示篩選包含時間篩選和進階篩選。 時間篩選可用來依事件時間戳記篩選追蹤結果，而進階篩選可用來透過事件欄位和動作建構篩選條件。 時間篩選和進階篩選之間有邏輯 AND 關聯性。  
  
#### <a name="to-create-a-filter"></a>若要建立篩選  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱，然後選取 **[監看即時資料]**。  
  
2.  在追蹤結果視窗中選取要篩選的結果，然後在擴充事件工具列上按一下 **[篩選]** 按鈕。  
  
3.  在 **[篩選]** 對話方塊中，選取 **[設定時間篩選]** 以透過拖曳滑動軸設定時間表來設定時間篩選。 請注意，在移動滑動軸時，時間方塊會顯示對應的時間值。 您也可以在時間方塊中輸入時間，或從下拉式清單中選取時間。 請注意，在輸入時間時，左側時間滑動軸會隨之移動。  
  
4.  在 **[其他篩選]** 區段中，套用篩選準則，然後按一下 **[套用]**。 完成建立篩選後，按一下 **[確定]**。  
  
 事件欄位與動作具有相同名稱時，則為特殊情況。 session_id 即為此情況的範例。 有幾個事件會包括 session_id 欄位，您也可以加入 session_id 動作。 已收集這兩項資訊，但擴充事件分析工具顯示方格會使用下列邏輯。  
  
-   此顯示方格中只會顯示一個資料行的複本 (在此案例中為 session_id)。  
  
-   如果資料中同時存在欄位和動作，則會顯示欄位值。  
  
-   如果資料中只存在欄位或動作，則會顯示欄位或動作。  
  
-   如果動作和欄位都不存在，則顯示 NULL。  
  
##  <a name="Search"></a> 搜尋資料行中的文字  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱，然後選取 **[監看即時資料]**。  
  
2.  在 [擴充事件] 工具列上，按一下 **[尋找]** 按鈕。  
  
3.  在 **[在擴充事件中尋找]** 對話方塊的 **[尋找目標]** 方塊中，輸入要搜尋的文字。  
  
     您可以從下拉式清單中選取最後 20 個搜尋字串的其中之一。  
  
4.  在 **[查詢]** 方塊中，從下拉式清單中選取要搜尋指定之文字的位置。 使用下列搜尋選項：  
  
    -   **資料表資料行**： 使用此選項可在追蹤視窗中搜尋所有可見資料行。  
  
    -   **詳細資料**： 使用此選項可在追蹤視窗中搜尋在開啟 **[在擴充事件中尋找]** 對話方塊之前已選取的所有資料行 (已升級和非升級)。  
  
    -   **\<事件資料行名稱 >**。 使用此選項可在下拉式清單的特定事件資料行中進行搜尋。  
  
5.  使用下列選項，指定定義搜尋的方式：  
  
    1.  **大小寫須相符**： 使用此選項可顯示與 **[尋找目標]** 方塊中輸入文字的內容和大小寫都相符的搜尋結果。  
  
    2.  **全字拼寫須相符**： 使用此選項即可僅顯示與輸入文字完全相符的搜尋結果。  
  
    3.  **向上搜尋**： 使用此選項可從游標位置開始搜尋至結果開頭。  
  
    4.  **使用**： 使用此選項可解譯 **[尋找目標]** 方塊中輸入的特殊字元和規則運算式。 特殊字元包含萬用字元 (*) 和 (?)，用於表示一個或多個字元。 規則運算式是用於定義搜尋文字模式的特殊標記法。  
  
6.  按一下 **[找下一個]** 可搜尋在 **[尋找目標]** 方塊中輸入的下一個文字。  
  
##  <a name="ChangeDisplay"></a> 變更顯示設定  
 您可以儲存資料行資訊 (資料行順序、合併資料行和資料行寬度)，並將追蹤結果的資訊篩選到「擴充事件」顯示設定檔案 (.viewsetting 檔案)。 在儲存檔案後，您可以將它套用到追蹤結果以變更檢視。  
  
#### <a name="to-change-the-display-settings"></a>若要變更顯示設定  
  
1.  開啟 .XEL 檔案以檢視追蹤結果  
  
    > [!NOTE]  
    >  您也可以用滑鼠右鍵按一下工作階段名稱，然後選取 **[監看即時資料]**。  
  
2.  在追蹤結果視窗的「擴充事件」工具列或功能表上，選取 **[顯示設定]**。  
  
3.  從下拉式清單中，選取下列其中一個選項：  
  
    -   **另存新檔**： 將追蹤結果的資料行和篩選資訊儲存為 .viewsetting 檔案。  
  
    -   **開啟**： 開啟現有的 .viewsetting 檔案。  
  
    -   **開啟最近使用的項目**： 開啟最近儲存的 .viewsetting 檔案。  
  
  