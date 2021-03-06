---
title: 監視 R 和 Python 處理程序-SQL Server Machine Learning 服務的擴充的事件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 96b791d98aa7fee588e4f72b76a733f48917f77a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642364"
---
# <a name="extended-events-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning 服務的擴充的事件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 提供一組相關的疑難排解操作中使用擴充事件[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，以及 Python 或 R 工作傳送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 Machine Learning 服務

## <a name="sql-server-events-for-machine-learning"></a>適用於 machine learning 的 SQL Server 事件

若要檢視 SQL Server 相關事件的清單，請從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行以下查詢。

```sql
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

如需使用擴充的事件的一般資訊，請參閱[擴充事件工具](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)。

> [!TIP]
> SQL Server 所產生的擴充事件，請試著新[SSMS XEvent 分析工具](https://docs.microsoft.com/sql/relational-databases/extended-events/use-the-ssms-xe-profiler)。 這項新功能在 Management Studio 中的會顯示擴充事件的即時檢視器，並較不干擾到 SQL Server 較類似的 Profiler 追蹤。

## <a name="additional-events-specific-to-machine-learning-components"></a>機器學習服務元件特有的其他事件

額外的擴充的事件可供與並使用 SQL Server Machine Learning 服務，例如元件[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，和 BXLServer，啟動 R 執行階段的附屬處理序。 這些額外擴充的事件從外部處理序中，會引發，因此您必須擷取使用外部的公用程式。

如需如何執行這項操作的詳細資訊，請參閱節[從外部處理序收集事件](#bkmk_externalevents)。

##  <a name="bkmk_xeventtable"></a> 擴充事件列表

|Event - 事件|描述|注意|  
|-----------|-----------------|---------|  
|connection_accept|接受新連線時會發生。 此事件是用來記錄所有的連線嘗試。||  
|failed_launching|啟動失敗。|表示發生錯誤。|  
|satellite_abort_connection|中止連接記錄||  
|satellite_abort_received|透過附屬連線收到中止訊息時引發。||  
|satellite_abort_sent|透過附屬連線傳送中止訊息時引發。||  
|satellite_authentication_completion|完成透過 TCP 或 Namedpipe 連線的驗證時引發。||  
|satellite_authorization_completion|完成透過 TCP 或 Namedpipe 連線的授權時引發。||  
|satellite_cleanup|清除附屬呼叫時引發。|只會從外部處理序引發。 檢視從外部處理序收集事件的指示。|  
|satellite_data_chunk_sent|附屬連線完成傳送單一資料區塊時引發。|事件會回報已傳送的資料列數、資料行數、已使用的 SNI 封包數，以及傳送區塊時所經過的時間 (以毫秒為單位)。 此資訊可協助您了解傳送不同類型的資料花費多少時間，以及使用多少封包。|  
|satellite_data_receive_completion|透過附屬連線收到查詢要求的所有資料時引發。|只會從外部處理序引發。 檢視從外部處理序收集事件的指示。|  
|satellite_data_send_completion|透過附屬連線傳送工作階段要求的所有資料時引發。||  
|satellite_data_send_start|開始資料傳輸時引發。| 在傳送第一個資料區塊前，就會開始資料傳輸。|  
|satellite_error|用來追蹤 SQL 附屬錯誤||  
|satellite_invalid_sized_message|訊息的大小無效||  
|satellite_message_coalesced|用來追蹤網路層的訊息聯合||  
|satellite_message_ring_buffer_record|訊息信號緩衝區記錄||  
|satellite_message_summary|訊息傳遞的相關摘要資訊||  
|satellite_message_version_mismatch|訊息的版本欄位不相符||  
|satellite_messaging|用來追蹤訊息事件 (繫結、解除繫結等)||  
|satellite_partial_message|用來追蹤網路層的部分訊息||  
|satellite_schema_received|在 SQL 收到並讀取結構描述訊息時引發。||  
|satellite_schema_sent|透過附屬處理序傳送結構描述訊息時引發。|只會從外部處理序引發。 檢視從外部處理序收集事件的指示。|  
|satellite_service_start_posted|在服務啟動訊息張貼到啟動控制板時引發。|這會通知啟動控制板啟動外部處理序，且其中包含新工作階段的識別碼。|  
|satellite_unexpected_message_received|收到非預期的訊息時引發。|表示發生錯誤。|  
|stack_trace|在要求處理序的記憶體傾印時發生。|表示發生錯誤。|  
|trace_event|用來進行追蹤|這些事件可以包含 SQL Server、啟動控制板和外部處理序追蹤訊息。 包含從 R 輸出至 stdout 和 stderr。|  
|launchpad_launch_start|啟動板開始啟動附屬處理序時引發。|只能從啟動控制板引發。 檢視從 launchpad.exe 收集事件的指示。|  
|launchpad_resume_sent|啟動控制板啟動附屬處理序並將繼續訊息傳送至 SQL Server 時引發。|只能從啟動控制板引發。 檢視從 launchpad.exe 收集事件的指示。|  
|satellite_data_chunk_sent|附屬連線完成傳送單一資料區塊時引發。|包含有關資料行數目、資料列數目、封包數目及傳送區塊所經過之時間的資訊。|  
|satellite_sessionId_mismatch|非預期的訊息工作階段識別碼||  
  
###  <a name="bkmk_externalevents"></a> 從外部處理序收集事件

SQL Server Machine Learning 服務會啟動一些在 SQL Server 處理序外部執行的服務。 若要擷取這些外部處理序的相關事件，您必須建立的事件追蹤設定檔，並將檔案放在與此程序的可執行檔相同的目錄中。  
  
+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    若要擷取與 Launchpad 相關的事件，請將 *.config* 檔案放在 SQL Server 執行個體的 Binn 目錄中。  在預設安裝中，這會是：

    `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`.  
  
+ **BXLServer**是支援外部指令碼語言，例如 R 或 Python 的 SQL 擴充性的附屬處理序。 BxlServer 的個別執行個體就會啟動每個外部語言執行個體。
  
    若要擷取與 BXLServer 相關的事件，請將 *.config* R 或 Python 安裝目錄中的檔案。  在預設安裝中，這會是：
     
    **R** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`。  

    **Python:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\library\RevoScaleR\rxLibs\x64`。

組態檔必須具有相同名稱與可執行檔，使用格式"[名稱].xevents.xml"。 也就是說，檔案必須用以下的格式命名︰

+ `Launchpad.xevents.xml`
+ `bxlserver.xevents.xml`

組態檔本身的格式如下：

```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="[session name]" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="you">Xevent for launchpad or bxl server.</description>  
    <event package="SQLSatellite" name="[XEvent Name 1]" />  
    <event package="SQLSatellite" name="[XEvent Name 2]" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="[SessionName].xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ 若要設定追蹤，請編輯*工作階段名稱*預留位置、 檔案名稱的預留位置 (`[SessionName].xel`)，以及您想要擷取，比方說，事件名稱`[XEvent Name 1]`， `[XEvent Name 1]`)。  
+ 任何數目的事件封裝標記可能會出現，而且只要 name 屬性正確無誤不會收集。

### <a name="example-capturing-launchpad-events"></a>範例擷取啟動控制板事件

下列範例會顯示為 Launchpad 服務的事件追蹤的定義：

```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="launchpad_launch_start" />  
    <event package="SQLSatellite" name="launchpad_resume_sent" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="launchpad_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ 將 *.config* 檔案放在 SQL Server 執行個體的 Binn 目錄中。
+ 這個檔案必須命名為`Launchpad.xevents.xml`。

### <a name="example-capturing-bxlserver-events"></a>範例擷取 BXLServer 事件  

以下範例顯示 BXLServer 可執行檔的事件追蹤。
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
 <event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="satellite_abort_received" />  
    <event package="SQLSatellite" name="satellite_authentication_completion" />  
    <event package="SQLSatellite" name="satellite_cleanup" />  
    <event package="SQLSatellite" name="satellite_data_receive_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_start" />  
    <event package="SQLSatellite" name="satellite_schema_sent" />   
    <event package="SQLSatellite" name="satellite_unexpected_message_received" />    
    <event package="SQLSatellite" name="satellite_data_chunk_sent" />   
    <target package="package0" name="event_file">  
      <parameter name="filename" value="satellite_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ 將 *.config* 檔案放在 BXLServer 可執行檔所在的相同目錄中。
+ 這個檔案必須命名為`bxlserver.xevents.xml`。

## <a name="see-also"></a>另請參閱

[Machine Learning 服務的自訂的 Management Studio 報表](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
