---
title: "INDEXPROPERTY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INDEXPROPERTY
- INDEXPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INDEXPROPERTY function
- indexes [SQL Server], viewing
- indexes [SQL Server], properties
ms.assetid: 998d5788-4871-44a8-8125-0d9390868b84
caps.latest.revision: 56
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cbd10b32ee6b2d88a97222c3a970452a4a628b83
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="indexproperty-transact-sql"></a>INDEXPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定資料表識別碼、索引或統計資料名稱以及屬性名稱的具名索引或統計資料屬性值。 如果是 XML 索引，則傳回 NULL。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
INDEXPROPERTY ( object_ID , index_or_statistics_name , property )   
```  
  
## <a name="arguments"></a>引數  
 *object_ID*  
 這是包含要提供的索引屬性資訊所屬之資料表或索引檢視之物件識別碼的運算式。 *object_ID*是**int**。  
  
 *index_or_statistics_name*  
 這是包含傳回屬性資訊所屬之索引或統計資料名稱的運算式。 *index_or_statistics_name*是**nvarchar （128)**。  
  
 *屬性*  
 這是包含要傳回之資料庫屬性名稱的運算式。 *屬性*是**varchar （128)**，而且可以是下列值之一。  
  
> [!NOTE]  
>  除非有說明，否則為 NULL 時，會傳回*屬性*不是有效的屬性名稱， *object_ID*不是有效的物件識別碼、 *object_ID*是不支援的物件類型指定的屬性，或者呼叫端沒有檢視物件的中繼資料的權限。  
  
|屬性|Description|值|  
|--------------|-----------------|-----------|  
|**IndexDepth**|索引的深度。|索引層級的數目。<br /><br /> NULL = XML 索引或輸入無效。|  
|**Indexdepth**|當建立索引或上次重建索引時，所用的填滿因數值。|填滿因數|  
|**IndexID**|指定的資料表或索引檢視之索引的索引識別碼。|Index ID|  
|**IsAutoStatistics**|ALTER DATABASE 的 AUTO_CREATE_STATISTICS 選項所產生的統計資料。|1 = True<br /><br /> 0 = False 或 XML 索引。|  
|**IsClustered**|索引已建立叢集。|1 = True<br /><br /> 0 = False 或 XML 索引。|  
|**IsDisabled**|索引已停用。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 輸入無效。|  
|**IsFulltextKey**|索引是資料表的全文檢索和語意索引鍵。|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = True<br /><br /> 0 = False 或 XML 索引。<br /><br /> NULL = 輸入無效。|  
|**IsHypothetical**|索引是假設的，無法直接當作資料存取路徑來使用。 假設的索引用來存放資料行層級的統計資料，由 Database Engine Tuning Advisor 來維護和使用。|1 = True<br /><br /> 0 = False 或 XML 索引<br /><br /> NULL = 輸入無效。|  
|**IsPadIndex**|索引指定每個內部節點保留開啟狀態的空間。|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = True<br /><br /> 0 = False 或 XML 索引。|  
|**IsPageLockDisallowed**|ALTER INDEX 的 ALLOW_PAGE_LOCKS 選項所設定的頁面鎖定值。|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 不允許頁面鎖定。<br /><br /> 0 = 允許頁面鎖定。<br /><br /> NULL = 輸入無效。|  
|**IsRowLockDisallowed**|ALTER INDEX 的 ALLOW_ROW_LOCKS 選項所設定的資料列鎖定值。|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 不允許資料列鎖定。<br /><br /> 0 = 允許資料列鎖定。<br /><br /> NULL = 輸入無效。|  
|**IsStatistics**|*index_or_statistics_name*是由 CREATE STATISTICS 陳述式或 ALTER DATABASE 的 AUTO_CREATE_STATISTICS 選項所建立的統計資料。|1 = True<br /><br /> 0 = False 或 XML 索引。|  
|**IsUnique**|索引是唯一的。|1 = True<br /><br /> 0 = False 或 XML 索引。|  
|**IsColumnstore**|索引是 xVelocity 記憶體最佳化的資料行存放區索引。|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = True<br /><br /> 0 = False|  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="exceptions"></a>例外狀況  
 當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。  
  
 使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，INDEXPROPERTY) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回的值**IsClustered**， **IndexDepth**，和**Indexdepth**屬性`PK`_`Employee` \_`BusinessEntityID`索引`Employee`資料表中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫。  
  
```  
SELECT   
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IsClustered')AS [Is Clustered],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexDepth') AS [Index Depth],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexFillFactor') AS [Fill Factor];  
  
```  
  
 以下為結果集：  
  
```  
Is Clustered Index Depth Fill Factor   
------------ ----------- -----------   
1            2           0  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會檢查其中一個索引的屬性上`FactResellerSales`資料表。  
  
```  
-- Uses AdventureWorks  
  
SELECT   
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsClustered') AS [Is Clustered],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsColumnstore') AS [Is Columnstore Index],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IndexFillFactor') AS [Fill Factor];  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [統計資料](../../relational-databases/statistics/statistics.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

