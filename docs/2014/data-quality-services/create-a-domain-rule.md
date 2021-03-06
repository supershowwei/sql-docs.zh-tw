---
title: 建立定義域規則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.rules.f1
- sql12.dqs.dm.testdomainrule.f1
ms.assetid: 339fa10d-e22c-4468-b366-080c33f1a23f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0e9f04742bbfabcfa0e351f25e9475a8022689e6
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65481036"
---
# <a name="create-a-domain-rule"></a>建立定義域規則
  本主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中建立定義域規則。 定義域規則是用來驗證、更正並標準化定義域值的條件。 定義域規則必須在定義域中成立，才能讓定義域值被視為正確且符合商務需求。 定義域規則所包含的驗證規則可用來驗證定義域值，但是無法用來更正資料品質專案中的資料。 此外，規則也包含針對有效資料套用以及用於資料更正的標準化規則。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要建立定義域規則，您必須已在 [定義域管理] 活動中開啟知識庫和定義域。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_administrator 角色，才能建立定義域規則。  
  
##  <a name="Build"></a> 建置定義域規則  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，開啟或建立知識庫。 選取 **[定義域管理]** 當做活動，然後按一下 **[開啟]** 或 **[建立]**。 如需相關資訊，請參閱 [建立知識庫](../../2014/data-quality-services/create-a-knowledge-base.md) 或 [開啟知識庫](../../2014/data-quality-services/open-a-knowledge-base.md)。  
  
    > [!NOTE]  
    >  定義域管理會在 Data Quality Services 用戶端的頁面上執行，該頁面包含個別定義域管理作業所適用的五個索引標籤。 這不是精靈驅動的程序，任何管理作業都可以個別執行。  
  
3.  從 **[定義域管理]** 頁面的 **[定義域清單]** 中，選取您想要建立定義域規則的定義域，或是建立新的定義域。 如果您必須建立新的定義域，請參閱＜ [建立定義域](../../2014/data-quality-services/create-a-domain.md)＞。  
  
4.  按一下 **[定義域規則]** 索引標籤。  
  
5.  按一下 **[加入新的定義域規則]**，然後輸入在知識庫中唯一的名稱以及規則的描述。  
  
6.  選取 **[使用中]** 指定將要執行此規則 (預設值)，或取消選取以防止執行此規則。  
  
7.  在 [建置規則] 窗格中，從規則子句方塊的下拉式清單中選取條件。  
  
8.  如果條件需要值，請在相關聯的文字方塊中輸入值。  
  
9. 如果需要另一個子句，請按一下 **[將新條件加入選取的子句]** 圖示。  
  
10. 選取 **[AND]** 或 **[OR]** 做為運算子。  
  
11. 必要時，請從下拉式清單中選取條件，然後輸入運算元的值。  
  
12. 若要變更子句出現在清單中的順序，請選取子句，然後按一下向上或向下箭號。 這樣就會變更子句的執行順序，但是可能會影響結果。  
  
13. 視需要加入其他子句。 如有需要，請選取子句，然後按一下 **[刪除選取的子句]**，藉以刪除子句。  
  
14. 視需要重複上述步驟，以便加入新的規則。  
  
15. 若要查看實作某個驗證規則之後對於值所產生的影響，請按一下 **[分析定義域規則對定義域值的影響]** 圖示。  
  
16. 繼續進行下列測試程序。  
  
##  <a name="Test"></a> 測試定義域規則  
  
1.  選取某項規則之後，按一下 **[在測試資料上執行選取的定義域規則]** 圖示。  
  
2.  在 [測試定義域規則] 對話方塊中，按一下 **[加入定義域規則的新測試詞彙]** 圖示。 輸入要測試的值。 視需要輸入其他值。 必要時，請選取一個值，然後按一下 **[移除選取的測試詞彙]** 圖示。  
  
3.  按一下 **[對所有詞彙測試定義域規則]** 圖示。  
  
4.  檢查每個詞彙的有效性。 核取記號表示「正確」、交叉表示「錯誤」，而三角形則表示「無效」。  
  
5.  完成測試對話方塊中的作業時，請按一下 **[關閉]** 。  
  
6.  視需要針對其他規則重複上述步驟。  
  
7.  繼續進行下列套用程序。  
  
##  <a name="Apply"></a> 套用定義域規則  
  
1.  按一下 **[套用所有規則]** ，將規則套用至定義域中的值。 當您按一下 **[套用所有規則]** 之後，系統就會顯示一個快顯視窗，其中指出處於特定狀態的多少值將會受到此規則所影響。 如果您仍然想要套用規則，請按一下 **[是]** ，否則請按一下 **[否]** 。 如果您按一下 **[是]**，請按一下 **[確定]** 關閉結果快顯視窗。  
  
    > [!NOTE]  
    >  當您建立或變更規則時，不需要儲存變更。 不過，您必須套用規則，才能讓變更生效。  
  
2.  按一下 **[放棄所有變更]** 移除您對定義域規則所做的任何變更，並還原成先前套用的規則，結果就是上次套用規則之後所做的任何變更將不再套用。 定義域中每個值的有效性將會更新成符合先前套用的規則，而非放棄的變更。  
  
3.  按一下 **[完成]** ，完成定義域管理活動，如＜ [結束定義域管理活動](../../2014/data-quality-services/end-the-domain-management-activity.md)＞中所述。  
  
##  <a name="FollowUp"></a> 後續操作：建立定義域規則之後  
 在建立定義域規則之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../../2014/data-quality-services/managing-a-domain.md)或[建立比對原則](../../2014/data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="Conditions"></a> 定義域規則條件  
 下表描述的是可在定義域規則中套用的條件，並且提供範例以說明如何套用這些條件。  
  
 當您套用定義域規則，但是某個定義域值使規則失敗時，該值就會被指定為無效。 如果導致值變成無效的規則已刪除、已停用或者已變更，讓該值不再使規則失敗，則指定為無效的值將會變更為正確。 如果您手動將某個值指定為無效 (在 [定義域管理] 活動的 [定義域值] 索引標籤中)，而且該值使之失敗的規則已經刪除、停用或變更，則該值仍然會被指定為無效 (符合手動指定)。  
  
 具有最終條件的定義域規則會將規則邏輯套用至一個或多個條件中值的同義字，以及值本身。 最終條件包括 [值等於]、[值不等於]、[值在] 或 [值不在]。 例如，假設您擁有下列定義域規則：「對於 'City' 而言，值等於 'Los Angeles'」。 如果 'Los Angeles' 和 'LA' 是同義字，則這兩個值都是正確的。 另一方面，如果您的規則並未包含最終條件，例如「對於 City 而言，值結尾為 "s"」，則 "Los Angeles" 是正確的，但是其同義字 "LA" 就會產生錯誤。  
  
 您可以在建立定義域規則時選擇其他替代方式。 例如，若要驗證值的開頭是否為 A、B 或 C 字母，您可以建立包含複雜條件的簡單規則 (例如包含縱線字元的規則運算式)，也可以建立包含許多簡單條件的複雜規則。 第一項規則的範例為「值包含規則運算式 (^A|^B|^C)」。 第二項規則的範例為「‘值開頭為 A' OR '值開頭為 B' OR '值開頭為 C'」。  
  
|條件|描述|範例|  
|---------------|-----------------|-------------|  
|長度等於|只有由運算元指定之字元數所組成的值才有效。|範例運算元：3<br /><br /> 有效值：BB1<br /><br /> 無效值：AA|  
|長度大於或等於|只有由運算元指定之字元數或更多字元數所組成的值才有效。|範例運算元：3<br /><br /> 有效的值：BB1、BBAA<br /><br /> 無效值：AA|  
|長度小於或等於|只有由運算元指定之字元數或更少字元數所組成的值才有效。|範例運算元：3<br /><br /> 有效的值：BB1、AA<br /><br /> 無效值：BBAA|  
|值等於|只有與運算元完全相同的值才有效。|範例運算元：BB1<br /><br /> 有效值：BB1<br /><br /> 無效值：BB, BB1#|  
|值不等於|只有與運算元不相同的值才有效。|範例運算元：BB1<br /><br /> 有效值：BB, BB1#<br /><br /> 無效值：BB1|  
|值包含|只有其所有字元以任何順序包含在運算元中的值才有效。|範例運算元：A1<br /><br /> 有效的值：A1, AA1<br /><br /> 無效值：1A、AA|  
|值不包含|只有不包含在運算元中的值才有效。|範例運算元：A1<br /><br /> 有效的值：1A、AA<br /><br /> 無效值：A1, AA1|  
|值開頭為|只有開頭為運算元中之字元的值才有效。|範例運算元：AA<br /><br /> 有效的值：AA1<br /><br /> 無效值：1AAB|  
|值結尾為|只有結尾為運算元中之字元的值才有效。|範例運算元：AA<br /><br /> 有效的值：1AA<br /><br /> 無效值：1AAB|  
|值是數字|只有具有 SQL Server 數值資料類型的值才有效。 這包括 int、decimal、float 等等。|範例運算元：N/A<br /><br /> 有效的值：1、25、345.1234<br /><br /> 無效值：2b、bcdef|  
|值為日期/時間|只有具有 SQL Server 日期/時間資料類型的值才有效。 這包括 datetime、time、date 等等。|範例運算元：N/A<br /><br /> 有效的值：1916-06-04；1916-06-04 18:24:24；March 21, 2001；5/18/2011；18:24:24<br /><br /> 無效值：March 213, 2006|  
|值在|只有位於運算元之集合中的值才有效。<br /><br /> 若要在集合中輸入值，請按一下運算元文字方塊、輸入第一個值、按下 Enter、輸入第二個值、針對您想要在集合中輸入的值重複上述步驟，然後再次按一下運算元文字方塊。 DQS 將會在集合中的值之間加入逗號。 如果您輸入包含逗號但不包含歸位字元的單一字串 (例如 "A1, B1")，DQS 就會將該字串視為集合中的單一值。|範例運算元：[A1, B1]<br /><br /> 有效的值：A1, B1<br /><br /> 無效值：AA, 11|  
|值不在|只有不在運算元之集合中的值才有效。|範例運算元：[A1, B1]<br /><br /> 有效的值：AA, 11<br /><br /> 無效值：A1, B1|  
|值符合模式|只有符合運算元中之字元、數字和特殊字元模式的值才有效。<br /><br /> 任何字母 (A...Z) 都可以當做任何字母的模式使用；不區分大小寫。 任何數字 (0...9) 都可以當做任何數字的模式使用。 除了字母或數字之外，任何特殊字元都可以當做其本身的模式使用。 方括號 [] 用於定義選擇性比對。|範例運算元：AA:000 (「任」兩個字元後面接著冒號 (:) 的模式，後面同樣再接著「任」三個數字)。<br /><br /> 有效的值：AB:012、df:257<br /><br /> 無效值：abc:123、FJ-369<br /><br /> 如需 DQS 與範例中模式規則的詳細資訊，請參閱 [DQS 定義域規則的模式比對](https://blogs.msdn.com/b/dqs/archive/2012/10/08/pattern-matching-in-dqs-domain-rules.aspx)。|  
|值不符合模式|只有不符合運算元中之字元、數字和特殊字元模式的值才有效。|範例運算元：A1 (值不得符合「任」一個字元後面接著「任」一個數字的模式)。<br /><br /> 有效的值：AB1、A、A:5<br /><br /> 無效值：B7、c9|  
|值包含模式|只有包含運算元中之字元、數字和特殊字元模式的值才有效。|範例運算元：AA-12 (值包含「任」兩個字元後面接著連字號 (-) 的模式，後面同樣再接著「任」兩個數字)。<br /><br /> 有效的值：AAA-01、ab-975<br /><br /> 無效值：A7、AA-6、C-45、aa;98|  
|值不包含模式|只有不包含運算元中之字元模式的值才有效。|範例運算元：AB-12 (值包含「任」兩個字元後面接著連字號 (-) 的模式，後面同樣再接著「任」兩個數字)。<br /><br /> 有效的值：A7、AA-6、C-45、aa;98<br /><br /> 無效值：AAA-01、ab-975|  
|值符合規則運算式|只有等於運算元中之規則運算式的值才會被視為有效。<br /><br /> 請勿在規則運算式中加入 "^" 錨點或 "$" 錨點，因為 DQS 會自動將這些錨點加入至包含「值等於規則運算式」的子句 (或者，您也可以使用括號來括住包含 "^" 和 "$" 錨點的規則運算式)。如需有關規則運算式的詳細資訊，請參閱＜ [規則運算式語言項目](https://go.microsoft.com/fwlink/?LinkId=225561)＞。|範例運算元：[1-5]+ (每個字元都必須是介於 1 到 5 之間的數字，並出現一次或多次)<br /><br /> 有效的值：123、12345、14352<br /><br /> 無效值：456、ABC|  
|值不符合規則運算式|只有不符合運算元中之規則運算式的值才會被視為有效。|範例運算元：[1-5]+ (字串不得只包含介於 1 到 5 之間的數字)<br /><br /> 有效的值：456、ABC<br /><br /> 無效值：123、123456、14352|  
  
  
