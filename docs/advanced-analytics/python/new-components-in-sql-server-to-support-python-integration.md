---
title: "Python 與 SQL Server 的整合元件 |Microsoft 文件"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 07f8e18b4481b2773f3ac16cdea08c27feff1ba3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="components-in-sql-server-to-support-python-integration"></a>若要支援 Python 整合 SQL Server 中的元件

機器學習服務從 SQL Server 2017，做為外部語言，可以從 T-SQL、 執行或執行當成計算內容使用遠端 SQL Server 支援 Python。

本主題特別說明在一般情況下支援擴充性的 SQL Server 2017 和 Python 語言中的元件。

## <a name="sql-server-components-and-providers"></a>SQL Server 元件和提供者

若要設定為允許 Python 指令碼執行的 SQL Server 2017 是多步驟程序。

1. 安裝擴充功能。
2. 啟用外部指令碼執行功能。
3. 重新啟動 database engine 服務。

可能需要額外的步驟，以支援遠端指令碼執行。

如需詳細資訊，請參閱[設定機器學習服務](setup-python-machine-learning-services.md)

### <a name="launchpad"></a>Launchpad

SQL Server 受信任的啟動列 是管理和執行外部指令碼，全文檢索索引和查詢服務，啟動處理全文檢索查詢的個別的主控件的方式類似，SQL Server 2016 中引進的服務。

Launchpad 服務可以啟動只信任的 launchers，Microsoft 所發行，或，經過 Microsoft 以符合需求，對效能與資源管理。

+ SQL Server 2017 支援 R 和 Python 3.5
+ SQL Server 2016 支援 R

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務在其自有的使用者帳戶下執行。

> [!TIP]
> 如果您變更執行 [啟動列] 的帳戶，請務必執行動作，以便使用 SQL Server 組態管理員，以確保變更會寫入相關檔案。

若要執行工作，以支援特定的語言，[啟動列] 會從集區，取得受保護的背景工作帳戶，並啟動附屬處理序來管理外部執行階段：

+ R 語言 rlauncher.dll 初始化
+ Python 3.5 Pythonlauncher.dll

每個附屬處理序繼承 Launchpad 的使用者帳戶，而且指令碼執行期間使用背景工作帳戶。 如果 Python 指令碼會使用平行處理，會建立相同且單一的背景工作帳戶。

[啟動列] 的安全性內容的相關資訊，請參閱[安全性](security-overview-sql-server-python-services.md)。

### <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL 附屬項目

如果您執行[處理序總管](https://technet.microsoft.com/sysinternals/processexplorer.aspx)Python 工作執行時，您可能會看到 BxlServer 的一個或多個執行個體。

**BxlServer**管理之間的通訊的 Microsoft 所提供的是可執行檔[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和 Python （或 R）。 它會建立 Windows 作業物件用來包含外部指令碼工作階段中，為每個外部指令碼工作中，佈建安全工作資料夾，並使用 SQL 附屬項目來管理外部執行階段之間的資料傳輸和[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。

實際上，BxlServer 是搭配的 Python[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]傳輸資料和管理工作。 BXL 代表二進位交換語言，然後使用 SQL Server 和外部處理序之間的有效率地移動資料的資料格式。 BxlServer 也是 Microsoft R 用戶端與 Microsoft R Server 很重要的一部分。

**SQL 附屬**起支援外部程式碼的 SQL Server 2016 資料庫引擎中包含的擴充性 API 或外部執行階段使用 C 或 c + + 實作。

BxlServer 將 SQL Satellite 用於下列工作：

+ 讀取輸入資料
+ 寫入輸出資料
+ 取得輸入引數
+ 寫入輸出引數
+ 錯誤處理
+ 將 STDOUT 和 STDERR 寫回用戶端

SQL 附屬項目使用自訂的資料格式之間的快速資料傳輸的最佳化[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和外部指令碼語言。 它會執行類型轉換，並定義輸入和輸出資料集的結構描述之間的通訊期間[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和外部指令碼執行階段。

使用擴充事件 (xEvents) 的 windows 可監視 SQL 附屬項目。 如需詳細資訊，請參閱[R 的擴充事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)。

## <a name="communication-channels-between-components"></a>元件之間的通訊通道

+ **TCP/IP**

  根據預設，之間的內部通訊[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和 SQL 附屬項目使用 TCP/IP。

+ **具名管道**

  BxlServer 和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之間透過 SQL Satellite 的內部資料傳輸，會使用專屬的壓縮資料格式來加強效能。 使用具名管道的 BXL 格式 Python 和 BxlServer 之間交換資料。

+ **ODBC**

  外部資料科學用戶端之間的通訊和[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]執行個體使用 ODBC。 傳送指令碼的帳戶作業至[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]必須有兩個權限連接到執行個體，並執行外部指令碼。

  此外，根據的工作，該帳戶可能需要這些權限：

  + 讀取作業所使用的資料
  + 寫入資料至資料表： 例如，當儲存結果儲存至資料表
  + 建立資料庫物件： 例如，如果將外部指令碼儲存為新的預存程序的一部分。

  當[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]是當成計算內容從遠端用戶端，執行 Python 指令碼和 Python 可執行檔必須從外部來源擷取資料，ODBC 會使用回寫。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]將遠端命令發出至目前的執行個體上的使用者身分識別的使用者的身分識別對應，並執行 ODBC 命令使用該使用者的認證。 執行此 ODBC 呼叫所需的連接字串可從用戶端程式碼取得。

## <a name="interaction-of-components"></a>元件的互動

下列圖表描述 SQL Server 元件互動的 Python 執行階段中每一個支援的案例： 使用 SQL Server 計算內容的 Python 終端機從執行中的資料庫和遠端執行指令碼。

### <a name="python-scripts-executed-in-database"></a>執行資料庫中的 Python 指令碼

當您執行 「 內部 」 的 Python [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，您必須將封裝的 Python 指令碼內的特殊的預存程序， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

指令碼包含已內嵌在預存程序之後，可以進行呼叫的預存程序的任何應用程式可以初始化執行 Python 程式碼。  此後[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]管理程式碼執行，在下圖將摘要說明。

![指令碼中 db python](../../advanced-analytics/python/media/script-in-db-python.png)

1. Python 執行階段的要求會以參數 _@language= 'Python'_傳遞至預存程序。 SQL Server Launchpad 服務来傳送此要求。
2. Launchpad 服務啟動適當的啟動器。在此情況下，PythonLauncher。
3. PythonLauncher 啟動外部 Python35 程序。
4. BxlServer 協調 Python 執行階段管理交換資料，與工作結果的儲存體。
5. SQL 附屬管理相關工作的通訊並處理具有[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
6. BxlServer 使用 SQL Satellite 來與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 進行狀態和結果的通訊。
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 會取得結果，並關閉相關工作和處理序。

### <a name="python-scripts-executed-from-a-remote-client"></a>從遠端用戶端執行 Python 指令碼

您可以從遠端電腦，例如膝上型電腦，執行 Python 指令碼，並將它們的 SQl Server 電腦的內容中執行，如果符合這些條件：

+ 您適當地設計指令碼
+ 遠端電腦已安裝的擴充程式庫所使用的機器學習服務

從遠端電腦傳送指令碼時下, 圖摘要說明整體的工作流程。

![遠端-sqlcc-從-python](../../advanced-analytics/python/media/remote-sqlcc-from-python2.png)

1. 中支援的函式**revoscalepy**，Python 執行階段呼叫連結的函式，也就會呼叫 BxlServer。
2. BxlServer 隨附機器學習服務 （資料庫），並且會在個別的處理序中執行來自 Python 執行階段。
3. BxlServer 決定連線目標，並初始使用 ODBC，傳遞認證提供的 Python 指令碼中的連接字串一部分的連接。
4. BxlServer 開啟對 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體的連線。
5. 呼叫的外部指令碼執行階段時，啟動控制板服務會叫用，以便依次啟動適當的啟動器： 在此情況下，PythonLauncher.dll。 之後，處理的 Python 程式碼時，處理類似於工作流程中的 Python 程式碼會叫用 T-SQL 中的預存程序。
6. PythonLauncher 會呼叫執行個體已安裝 Python[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]電腦。
7. 結果會傳回 BxlServer。
8. SQL Satellite 管理與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的通訊，並清理相關的工作物件。
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 將結果傳遞回用戶端。

## <a name="next-steps"></a>後續的步驟

[SQL Server 中的 python 架構概觀](architecture-overview-sql-server-python.md)