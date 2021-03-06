---
title: CREATE MEMBER 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 432438fe9a6e1b39c849188050b67f816d895187
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250212"
---
# <a name="mdx-data-definition---create-member"></a>MDX 資料定義 - CREATE MEMBER


  建立導出成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE [ SESSION ] [HIDDDEN] [ CALCULATED ] MEMBER CURRENTCUBE | Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供將建立成員之 Cube 名稱的有效字串運算式。  
  
 *Member_Name*  
 提供成員名稱的有效字串運算式。 指定完整名稱，以便在量值維度以外的維度中建立成員。 如果不提供完整成員名稱，則將在量值維度中建立成員。  
  
 *MDX_Expression*  
 有效的多維度運算式 (MDX) 運算式。  
  
 *Property_Name*  
 提供導出成員屬性名稱的有效字串。  
  
 *Property_Value*  
 定義導出成員屬性值的有效純量運算式。  
  
## <a name="remarks"></a>備註  
 CREATE MEMBER 陳述式定義的導出成員可在整個工作階段中使用，因此，亦可用於工作階段期間的多個查詢。 如需詳細資訊，請參閱 <<c0> [ 建立導出成員 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md)。</c0>  
  
 您也可以定義供單一查詢使用的導出成員。 若要定義受限於單一查詢的導出成員，您可以在 SELECT 陳述式中使用 WITH 子句。 如需詳細資訊，請參閱 <<c0> [ 建立查詢範圍導出成員 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)。</c0>  
  
 *Property_Name*可以參考其中一個標準或選擇性導出的成員屬性。 本主題稍後會列出標準成員屬性。 導出成員使用 CREATE MEMBER 而建立**工作階段**值有工作階段範圍。 此外，導出成員定義內的字串會以雙引號分隔。 這跟以 OLE DB 定義的方法不同，以 OLE DB 定義的方法指定以單引號來分隔字串。  
  
 指定目前連接之 Cube 以外的 Cube 會導致發生錯誤。 因此，您應該使用 CURRENTCUBE 取代 Cube 名稱，來代表目前的 Cube。  
  
 如需 OLE DB 定義之成員屬性的詳細資訊，請參閱 OLE DB 文件集。  
  
## <a name="scope"></a>範圍。  
 導出成員可發生在下表列出的其中一個範圍內。  
  
 查詢範圍  
 導出成員的可見性與存留期間受限於查詢。 導出成員是在個別查詢中定義。 查詢範圍可覆寫工作階段範圍。 如需詳細資訊，請參閱 <<c0> [ 建立查詢範圍導出成員 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)。</c0>  
  
 工作階段範圍  
 導出成員的可見性與存留期間受限於其建立所在的工作階段。 （存留時間小於工作階段期間如果導出成員上發出 DROP MEMBER 陳述式。）CREATE MEMBER 陳述式會以工作階段範圍建立導出的成員。  
  
### <a name="scope-isolation"></a>範圍隔離  
 當 Cube 多維度運算式 (MDX) 指令碼包含導出成員時，會預設為先解析導出成員後，再解析任何工作階段範圍的計算和任何查詢定義的計算。  
  
> [!NOTE]  
>  在某些情況下， [Aggregate (MDX)](../mdx/aggregate-mdx.md)函式並[VisualTotals (MDX)](../mdx/visualtotals-mdx.md)函式並不會出現這種行為。  
  
 該行為可讓一般用戶端應用程式使用包含複雜計算的 Cube，而不需考慮到計算的特定實作。 不過，在某些情況下，您可能想要執行工作階段或查詢範圍導出的成員之前特定計算中的 cube，但兩者都不**彙總**函式，也不**VisualTotals**函式皆適用。 若要完成此計算，使用 SCOPE_ISOLATION 計算屬性。  
  
#### <a name="example"></a>範例  
 下列指令碼是必須使用 SCOPE_ISOLATION 計算屬性才能產生正確結果的狀況範例。  
  
 **Cube 的 MDX 指令碼：**  
  
```  
CREATE MEMBER CURRENTCUBE.Measures.ProfitRatio AS 'Measures.[Store Sales]/Measures.[Store Cost]', SOLVE_ORDER = 10  
```  
  
 **MDX 查詢：**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
 上述查詢需要的結果是 USA 扣除 WA 後的銷售額與 USA 扣除 WA 後的 Store Cost 兩者的比率。 上述查詢不會傳回所需的結果，而會傳回 USA 扣除的比率與 WA 的比率，這是沒有意義的結果。 若要得到需要的結果，您可以使用 SCOPE_ISOLATION 計算屬性。  
  
 **使用 SCOPE_ISOLATION 計算屬性的 MDX 查詢：**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
,SCOPE_ISOLATION=CUBE  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
## <a name="standard-properties"></a>標準屬性  
 每個導出成員都有一組預設屬性。 當用戶端應用程式連接到[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，預設屬性是直接或可以受到支援，由系統管理員決定。  
  
 可能會有其他的成員屬性可用，視 Cube 定義而定。 以下屬性代表與 Cube 中維度層級相關的資訊。  
  
|屬性識別碼|意義|  
|-------------------------|-------------|  
|SOLVE_ORDER|當導出成員參考另一個導出成員 (亦即，導出成員彼此交叉) 時，解析導出成員的順序。|  
|FORMAT_STRING|顯示資料格的值時，用戶端應用程式可以使用 Office 樣式格式字串。|  
|VISIBLE|指出是否可以看見結構描述資料列集中導出成員的值。 可見的導出成員可以加入至一組[AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md)函式。 非零的值代表可以看見導出成員。 這個屬性的預設值是*Visible*。<br /><br /> 不可見的導出成員 (此值會設為零) 一般會在較為複雜的導出成員中作為中間步驟。 其他成員類型 (例如，量值) 也可以參考這些導出成員。|  
|NON_EMPTY_BEHAVIOR|解析空白資料格時，用以決定導出成員行為的量值或集合。<br /><br /> **\*\* 警告\* \*** 這個屬性已被取代。 請勿設定。 如需詳細資訊，請參閱 [SQL Server 2016 中已被取代的 Analysis Services 功能](../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) 。|  
|CAPTION|用戶端應用程式當做成員標題使用的字串。|  
|DISPLAY_FOLDER|識別用戶端應用程式用於顯示成員之顯示資料夾路徑的字串。 資料夾層級的分隔符號是由用戶端應用程式所定義。 工具和所提供的用戶端[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，反斜線 (\\) 為層級分隔符號。 若要針對已定義的成員提供多個顯示資料夾，請使用分號 (;) 來分隔資料夾。|  
|ASSOCIATED_MEASURE_GROUP|與此成員建立關聯之量值群組的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [DROP MEMBER 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [UPDATE MEMBER 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-update-member.md)   
 [MDX 資料定義陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
