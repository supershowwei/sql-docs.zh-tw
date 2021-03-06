---
title: SQLStatistics 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cd0503b9f0169a19179bcee545132279903ea10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62851610"
---
# <a name="sqlstatistics-function"></a>SQLStatistics 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLStatistics**擷取一份關於單一資料表與資料表相關聯的索引統計資料。 驅動程式會傳回資訊當作結果集。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *CatalogName*  
 [輸入]目錄名稱。 如果驅動程式支援的目錄，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有目錄的資料表。 *CatalogName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*CatalogName*是一般的引數; 也就是，則會視為和其案例很重要。 如需詳細資訊，請參閱 <<c0> [ 目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]中的字元長度 **CatalogName*。  
  
 *SchemaName*  
 [輸入]結構描述名稱。 如果驅動程式支援的結構描述，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有結構描述的資料表。 *SchemaName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *SchemaName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*SchemaName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength2*  
 [輸入]中的字元長度 **SchemaName*。  
  
 *TableName*  
 [輸入]資料表名稱。 此引數不可為 null 指標。 *SchemaName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *TableName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*TableName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength3*  
 [輸入]中的字元長度 **TableName*。  
  
 *唯一*  
 [輸入]索引的類型：SQL_INDEX_UNIQUE 或 SQL_INDEX_ALL。  
  
 *已保留*  
 [輸入]指出結果集中的基數和頁面資料行的重要性。 下列選項會影響傳回的基數和頁面資料行即使不會傳回基數和頁面，會傳回索引資訊。  
  
 SQL_ENSURE 要求驅動程式無條件地擷取統計資料。 （只符合 Open Group 標準，而且不支援的 ODBC 延伸模組的驅動程式將無法支援 SQL_ENSURE。）  
  
 SQL_QUICK 要求，此驅動程式擷取的基數和頁面才可以從伺服器提供。 在這個情況下，驅動程式無法確保這些值是否為最新的。 (撰寫 Open Group 標準的應用程式一律會從 ODBC 3 取得 SQL_QUICK 行為 *.x*-相容的驅動程式。)  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLStatistics**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLStatistics** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|資料指標是開啟*StatementHandle*，並**SQLFetch**或是**SQLFetchScroll**呼叫。 如果此錯誤會傳回由驅動程式管理員**SQLFetch**或是**SQLFetchScroll**尚未傳回 sql_no_data 之後，如果驅動程式傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 資料指標是開啟*StatementHandle*，但**SQLFetch**或是**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復，因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*，並接著呼叫函式上再次*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|使用無效的 null 指標|*TableName*引數是 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*引數為 null 指標，以及 SQL_CATALOG_NAME*資訊類型*支援的目錄名稱，傳回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，而*SchemaName*引數是 null 指標。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLStatistics**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 其中一個名稱的長度引數的值小於 0，但不是等於 SQL_NTS。<br /><br /> 其中一個名稱的長度引數的值超過最大長度值，對應的名稱。|  
|HY100|唯一性選項類型超出範圍|(DM) 無效*Unique*指定的值。|  
|HY101|精確度選項類型超出範圍|(DM) 無效*保留*指定的值。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定目錄，並在驅動程式或資料來源不支援目錄。<br /><br /> 已指定結構描述，且驅動程式或資料來源不支援結構描述。<br /><br /> 驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 陳述式屬性已設定為驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前要求的結果集傳回的資料來源。 透過設定的逾時期限**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLStatistics**傳回做為標準的結果集，按照 NON_UNIQUE 」、 「 類型 」、 「 INDEX_QUALIFIER 」、 「 INDEX_NAME 和 「 ORDINAL_POSITION 單一資料表的相關資訊。 結果集結合了統計資料中的資訊 （結果集的基數和頁面資料行） 資料表的每個索引的相關資訊。 如需如何使用這項資訊，請參閱[使用的目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 若要判斷 TABLE_CAT，再依據 table_schem 排列、 TABLE_NAME、 COLUMN_NAME 資料行的實際長度，應用程式可以呼叫**SQLGetInfo**搭配 SQL_MAX_CATALOG_NAME_LEN SQL_MAX_SCHEMA_NAME_LEN、 SQL_MAX_TABLE_NAME_LEN，和 SQL_MAX_COLUMN_NAME_LEN 選項。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 下列資料行已重新命名為 ODBC 3 *.x*。 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3 *.x*資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 下表列出結果集內的資料行。 驅動程式，可以定義資料行 13 (FILTER_CONDITION) 以外的其他資料行。 應用程式應該透過從結果集而不是指定明確的序數位置的結尾算起往下取得驅動程式特有的資料行權限。 如需詳細資訊，請參閱 <<c0> [ 目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|資料表的統計資料或索引套用至; 目錄名稱如果不適用於資料來源，則為 NULL。 如果驅動程式支援目錄對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 沒有目錄這些資料表。|  
|再依據 TABLE_SCHEM 排列 (ODBC 1.0)|2|Varchar|統計資料或索引套用至; 的資料表結構描述名稱如果不適用於資料來源，則為 NULL。 如果驅動程式支援結構描述對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 並沒有結構描述這些資料表。|  
|TABLE_NAME (ODBC 1.0)|3|非 NULL Varchar|資料表的統計資料或索引套用的資料表名稱。|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|指出是否索引不允許重複的值：<br /><br /> SQL_TRUE 如果可以為非唯一的索引值。<br /><br /> 如果索引值必須是唯一的 SQL_FALSE。<br /><br /> 如果型別是 SQL_TABLE_STAT，則傳回 NULL。|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|用來限定索引的識別碼名稱這麼做**DROP INDEX**;如果資料來源不支援索引限定詞或型別是 SQL_TABLE_STAT，則傳回 NULL。 如果此資料行中傳回非 null 值，則必須使用在限定的索引名稱**DROP INDEX**陳述式; 否則再依據 table_schem 排列應該用來限定的索引名稱。|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|索引名稱;如果型別是 SQL_TABLE_STAT，則傳回 NULL。|  
|型別 (ODBC 1.0)|7|Smallint 非 NULL|要傳回的資訊類型：<br /><br /> SQL_TABLE_STAT 表示 （中的基數或頁面的資料行） 之資料表的統計資料。<br /><br /> SQL_INDEX_BTREE 表示 B 型樹狀目錄索引。<br /><br /> SQL_INDEX_CLUSTERED 表示非叢集的索引。<br /><br /> SQL_INDEX_CONTENT 表示內容的索引。<br /><br /> SQL_INDEX_HASHED 表示雜湊的索引。<br /><br /> SQL_INDEX_OTHER 表示另一個索引類型。|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|索引 （從 1 開始）; 中的資料行序號如果型別是 SQL_TABLE_STAT，則傳回 NULL。|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|資料行名稱。 如果資料行根據運算式，例如薪資 + 權益，則會傳回運算式;如果無法判斷運算式，則會傳回空字串。 如果型別是 SQL_TABLE_STAT，則傳回 NULL。|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|資料行的排序順序："A"表示遞增;"D"表示遞減;如果資料來源不支援資料行排序順序或型別是 SQL_TABLE_STAT，則傳回 NULL。|  
|基數 (ODBC 1.0)|11|Integer|基數為資料表或索引;如果類型是 SQL_TABLE_STAT; 在資料表中的資料列數目如果類型不是 SQL_TABLE_STAT; 的索引中的唯一值數目如果值不是可從資料來源，則傳回 NULL。|  
|頁面 (ODBC 1.0)|12|Integer|用來儲存索引或資料表的頁面數目如果型別是 SQL_TABLE_STAT; 資料表的頁面數目如果類型不是 SQL_TABLE_STAT; 的索引的頁面數目如果值不是可從資料來源，或如果不適用於資料來源，則傳回 NULL。|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|如果索引是篩選的索引，這是篩選條件，例如 SALARY > 30000;如果無法判斷篩選條件，這會是空字串。<br /><br /> 如果索引不是已篩選的索引，則為 NULL，它無法判斷索引是篩選的索引，還是別 SQL_TABLE_STAT。|  
  
 如果結果集中的資料列會對應至資料表，驅動程式類型設定為 SQL_TABLE_STAT 並設定 NON_UNIQUE、 INDEX_QUALIFIER、 INDEX_NAME、 ORDINAL_POSITION、 COLUMN_NAME 和 ASC_OR_DESC 為 NULL。 如果基數或頁面未提供的資料來源，驅動程式會設定它們為 NULL。  
  
## <a name="code-example"></a>程式碼範例  
 類似的函式的程式碼範例，請參閱 < [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|正在提取單一資料列或順向方向中的資料區塊。|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回外部索引鍵資料行|[SQLForeignKeys 函式](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|傳回主索引鍵資料行|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
