---
title: 教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 051123efd5c58048635bb83e43eaff73218c463e
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241536"
---
# <a name="tutorial-getting-started-with-always-encrypted-with-secure-enclaves-using-ssms"></a>教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程將教導您如何開始使用[具有安全記憶體保護區的 Always Encrypted](encryption/always-encrypted-enclaves.md)。 它會顯示：
- 如何建立基本環境來測試和評估具有安全記憶體保護區的 Always Encrypted。
- 如何就地加密資料，以及使用 SQL Server Management Studio (SSMS) 針對加密資料行發出豐富的查詢。

## <a name="prerequisites"></a>Prerequisites

若要開始使用具有安全記憶體保護區的 Always Encrypted，您需要至少兩部電腦 (它們可以是虛擬機器)：

- SQL Server 電腦以裝載 SQL Server 和 SSMS。
- HGS 電腦以執行主機守護者服務，這是記憶體保護區證明所需。

### <a name="sql-server-computer-requirements"></a>SQL Server 電腦需求

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] 或更新版本。
- Windows 10 企業版 1809 版或 Windows Server 2019 Datacenter。
- 如果您的 SQL Server 電腦是實體機器，它必須符合 [HYPER-V 硬體需求](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/reference/hyper-v-requirements#hardware-requirements) \(部分機器翻譯\)：
   - 使用第二層位址轉譯 (SLAT) 的 64 位元處理器
   - 對 VM 監視器模式擴充功能的 CPU 支援 (Intel CPU 上的 VT-c)
   - 已啟用虛擬化支援 (Intel VT-x 或 AMD-V)
- 如果您的 SQL Server 電腦是虛擬機器，則必須將該 VM 設定為允許巢狀虛擬化。
   - 在 Hyper-V 2016 或更新版本上，在 VM 處理器上[啟用巢狀虛擬化擴充功能](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/user-guide/nested-virtualization#configure-nested-virtualization) \(部分機器翻譯\)。
   - 在 Azure 中，確定您正在執行支援巢狀虛擬化的 VM 大小，例如 Dv3 和 Ev3 系列的 VM。 請參閱[建立可使用巢狀功能的 Azure VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/nested-virtualization#create-a-nesting-capable-azure-vm) \(部分機器翻譯\)。
   - 在 VMWare vSphere 6.7 或更新版本上，針對 VM 啟用虛擬化型安全性支援，如 [VMware 文件](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-C2E78F3E-9DE2-44DB-9B0A-11440800AADD.html) \(英文\) 所述。
   - 其他 Hypervisor 和公用雲端可能支援在 VM 中使用具有安全記憶體保護區的 Always Encrypted，前提是已對 VM 公開虛擬化擴充 (又稱巢狀虛擬化)。 如需相容性和設定指示，請參閱您虛擬化解決方案的文件。
- [SQL Server Management Studio (SSMS) 18.0 或更新版本](../../ssms/download-sql-server-management-studio-ssms.md)。

或者，您也可以在另一部電腦上安裝 SSMS。

>[!WARNING] 
>在生產環境中，您絕不應該使用 SSMS 或其他工具來管理 Always Encrypted 金鑰，或對 SQL Server 電腦上的加密資料執行查詢，因為這樣可能會降低或完全損害使用 Always Encrypted 的目的。

### <a name="hgs-computer-requirements"></a>HGS 電腦需求

- Windows Server 2019 Standard 或 Datacenter Edition
- 2 個 CPU
- 8 GB RAM
- 100 GB 儲存體

>[!NOTE]
>在您開始之前，不應該將 HGS 電腦加入網域。

## <a name="step-1-configure-the-hgs-computer"></a>步驟 1:設定 HGS 電腦

在此步驟中，您將設定 HGS 電腦以執行主機守護者服務，支援主機金鑰證明。

1. 以系統管理員 (本機系統管理員) 身分登入 HGS 電腦、開啟提升權限的 Windows PowerShell 主控台，並執行下列命令來新增主機守護者服務角色：

   ```powershell
   Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
   ```

2. HGS 電腦重新開機之後，再次使用您的系統管理員帳戶登入、開啟提升權限的 Windows PowerShell 主控台，並執行下列命令來安裝主機守護者服務和設定其網域。 您在此處指定的密碼只適用於 Active Directory 的目錄服務修復模式密碼；它不會變更您的系統管理員帳戶登入密碼。 您可以為 -HgsDomainName 提供您選擇的任何網域名稱。

   ```powershell
   $adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force
   Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
   ```

3. 再次重新啟動電腦之後，登入您的系統管理員帳戶 (這現在也是網域系統管理員)、開啟提高權限的 Windows PowerShell 主控台，並設定 HGS 執行個體的主機金鑰證明。 

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey  
   ```

4. 執行下列命令來尋找 HGS 電腦的 IP 位址。 儲存此 IP 位址，供後續步驟使用。

   ```powershell
   Get-NetIPAddress  
   ```

>[!NOTE]
>或者，如果您想要以 DNS 名稱來參考您的 HGS 電腦，可以設定從您公司 DNS 伺服器到新 HGS 網域控制站的轉寄站。  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>步驟 2:設定 SQL Server 電腦作為受防護主機
在此步驟中，您將設定 SQL Server 電腦作為使用主機金鑰證明來向 HGS 註冊的受防護主機。
>[!NOTE]
>主機金鑰證明只建議在測試環境中使用。 針對生產環境，您應該使用 TPM 證明。

1. 以系統管理員身分登入您的 SQL Server 電腦，開啟提升權限的 Windows PowerShell 主控台，然後透過存取 computername 變數來擷取您電腦的名稱。

   ```powershell
   $env:computername 
   ```

2. 安裝「受防護主機」功能，這也會安裝 Hyper-V (若尚未安裝的話)。

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

3. 提示時重新啟動 SQL Server 電腦，以完成安裝 Hyper-V。

4. 如果您的 SQL Server 電腦是虛擬機器，或者，其為不支援 UEFI 安全開機或未配備 IOMMU 的舊有實體機器，則您需要移除平台安全性功能的 VBS 需求。
    1. 在 Windows 登錄中移除該需求。

        ```powershell
       Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name RequirePlatformSecurityFeatures -Value 0
       ```

    1. 再次重新啟動電腦，以降低的需求使 VBS 上線。

        ```powershell
       Restart-Computer
       ```



4. 以系統管理員身分再次登入 SQL Server 電腦、開啟提升權限的 Windows PowerShell 主控台、產生唯一的主機金鑰，並將產生的公開金鑰匯出至檔案。

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

5. 將上一個步驟中產生的主機金鑰檔案手動複製到 HGS 電腦。 下列指示假設您的檔案名稱為 hostkey.cer，且您正在將它複製到 HGS 電腦上的桌面。

6. 在 HGS 電腦上，開啟提升權限的 Windows PowerShell 主控台，並向 HGS 註冊 SQL Server 電腦的主機金鑰：

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

7. 在 SQL Server 電腦上，在提升權限的 Windows PowerShell 主控台執行下列命令，以告知 SQL Server 電腦證明的位置。 請務必同時在兩個位址位置中指定 HGS 電腦的 IP 位址或 DNS 名稱。 

   ```powershell
   # use http, and not https
   Set-HgsClientConfiguration -AttestationServerUrl http://<IP address or DNS name>/Attestation -KeyProtectionServerUrl http://<IP address or DNS name>/KeyProtection/  
   ```

上述命令的結果應該顯示 AttestationStatus = Passed。

如果您收到 HostUnreachable 錯誤，就表示您的 SQL Server 電腦無法與 HGS 通訊。 請確定您可以 ping HGS 電腦。

UnauthorizedHost 錯誤指出公開金鑰未向 HGS 伺服器註冊 - 請重複步驟 5 和 6，以解決此錯誤。

如果所有其他方式均失敗，請執行 Clear-HgsClientHostKey，並重複步驟 4-7。

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>步驟 3：在 SQL Server 啟用具有安全記憶體保護區的 Always Encrypted

在此步驟中，您將在 SQL Server 執行個體中使用記憶體保護區啟用 Always Encrypted 的功能。

1. 開啟 SSMS、以系統管理員身分連線到您的 SQL Server 執行個體，並開啟新的查詢視窗。
2. 將安全記憶體保護區類型設定為虛擬化型安全性 (VBS)。

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

3. 重新啟動您的 SQL Server 執行個體，先前的變更才會生效。 您可以在 SSMS 中重新啟動執行個體，方法是在 [物件總管] 中以滑鼠右鍵按一下它，然後選取 [重新啟動]。 執行個體重新啟動之後，請與它重新連線。

4. 執行下列查詢，確認現在已載入安全記憶體保護區：

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    查詢應該會傳回下列結果：  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | 資料行加密記憶體保護區類型 | 1     | 1              |

5. 若要啟用對加密資料行的豐富計算，請執行下列查詢：

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > 在 [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] 中預設已停用豐富計算。 每次重新啟動 SQL Server 執行個體之後，需要使用上述陳述式予以啟用。

## <a name="step-4-create-a-sample-database"></a>步驟 4：建立範例資料庫
在此步驟中，您將建立一個具有部分範例資料的資料庫，且稍後會加密它。

1. 使用 SSMS 連線至 SQL Server 執行個體。
2. 建立新的資料庫，名為 ContosoHR。

    ```sql
    CREATE DATABASE [ContosoHR];
    ```

3. 確定您連線的是新建立的資料庫。 建立新的資料表，名為 Employees。

    ```sql
    USE [ContosoHR];
    GO
    
    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY];
    ```

4. 在 Employees 資料表中新增一些員工記錄。

    ```sql
    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692);
 
    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415);
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>步驟 5：佈建已啟用記憶體保護區的金鑰

在此步驟中，您將建立資料行主要金鑰和允許記憶體保護區計算的資料行加密金鑰。

1. 使用 SSMS 連線到您的資料庫。
2. 在 [物件總管] 中，展開您的資料庫，然後巡覽至 [安全性] > [Always Encrypted 金鑰]。
3. 佈建已啟用記憶體保護區的新資料行主要金鑰：
    1. 以滑鼠右鍵按一下 [Always Encrypted 金鑰]，然後選取 [新增資料行主要金鑰]。
    2. 選取您的資料行主要金鑰名稱：CMK1。
    3. 請確定您選取 [Windows 憑證存放區 (目前的使用者或本機電腦)] 或 [Azure Key Vault]。
    4. 選取 [允許記憶體保護區運算]。
    5. 如果您已選取 Azure Key Vault，請登入 Azure，然後選取您的金鑰保存庫。 如需如何建立 Always Encrypted 金鑰保存庫的詳細資訊，請參閱 [Manage your key vaults from Azure portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/) (從 Azure 入口網站管理金鑰保存庫)。
    6. 選取您的憑證或 Azure Key Vault 金鑰 (如果已經存在)，或按一下 [產生憑證] 按鈕來建立一個新的憑證。
    7. 選取 [確定]。

        ![允許記憶體保護區運算](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)
    
4. 建立已啟用記憶體保護區的新資料行加密金鑰：

    1. 以滑鼠右鍵按一下 [Always Encrypted 金鑰]，然後選取 [新增資料行加密金鑰]。
    2. 輸入新資料行加密金鑰的名稱：CEK1。
    3. 在 [資料行主要金鑰] 下拉式清單中，選取您在先前步驟中建立的資料行主要金鑰。
    4. 選取 [確定]。

## <a name="step-6-encrypt-some-columns-in-place"></a>步驟 6：就地加密某些資料行

在此步驟中，您會將伺服器端記憶體保護區內 SSN 和 Salary 資料行中儲存的資料加密，然後測試資料的 SELECT 查詢。

1. 在 SSMS 中，設定新的查詢視窗，並針對資料庫連線啟用 Always Encrypted 。
    1. 在 SSMS 中，開啟新的查詢視窗。
    2. 以滑鼠右鍵按一下新查詢視窗中的任何位置。
    3. 選取 [連線]\>[變更連線]。
    4. 選取 [選項]。 巡覽至 [Always Encrypted] 索引標籤，並選取 [啟用 Always Encrypted]，然後指定您的記憶體保護區證明 URL (例如，<span>http://</span>hgs.bastion.local/Attestation)。
    5. 選取 [連接]。
    6. 如果系統提示您啟用 Always Encrypted 的參數化查詢，按一下 [啟用]。
2. 在 SSMS 中，設定另一個查詢視窗，並針對資料庫連線停用 Always Encrypted 。
    1. 在 SSMS 中，開啟新的查詢視窗。
    2. 以滑鼠右鍵按一下新查詢視窗中的任何位置。
    3. 選取 [連線]\>[變更連線]。
    4. 選取 [選項]。 巡覽至 [Always Encrypted] 索引標籤，並確定未選取 [啟用 Always Encrypted]。
    5. 選取 [連接]。
    6. 將資料庫內容變更為 ContosoHR 資料庫。
1. 加密 SSN 和 Salary 資料行。 在已啟用 Always Encrypted 的查詢視窗中，貼上並執行以下指令碼：

    ```sql
    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11) COLLATE Latin1_General_BIN2
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);
     
    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);
 
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > 請注意上述指令碼中用來清除資料庫查詢計畫快取的 ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE 陳述式。 修改資料表之後，您需要清除所有批次之計畫和存取資料表的預存程序，以重新整理參數加密資訊。 

4. 若要確認 SSN 和 Salary 資料行現在已加密，請在查詢視窗中貼上並執行以下陳述式，並且停用 Always Encrypted。 查詢視窗應該在 SSN 和 Salary 資料行中傳回加密的值。 使用已啟用 Always Encrypted 的查詢視窗，嘗試相同的查詢，以查看解密的資料。

    ```sql
    SELECT * FROM [dbo].[Employees];
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>步驟 7：針對加密的資料行執行豐富查詢

現在，您可以針對加密的資料行執行豐富查詢。 在伺服器端記憶體保護區內，將會執行一些查詢處理。 

1. 確定會啟用 [Always Encrypted 的參數化]。
    1. 從 SSMS 的主功能表中，選取 [查詢]。
    2. 選取 [查詢選項]。
    3. 瀏覽至 [執行] > [進階]。
    4. 確定會勾選 [啟用 Always Encrypted 的參數化]。
    5. 選取 [確定]。
2. 在已啟用 Always Encrypted 的查詢視窗中，貼上並執行以下查詢。 查詢應該會傳回純文字值和符合指定搜尋準則的資料列。

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818';
    DECLARE @MinSalary [money] = $1000;
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```
3. 在未啟用 Always Encrypted 的查詢視窗中再次嘗試相同的查詢，並留意到隨即發生的失敗。

## <a name="next-steps"></a>Next Steps
請參閱[設定具有安全記憶體保護區的 Always Encrypted](encryption/configure-always-encrypted-enclaves.md)，以獲得關於其他使用案例的想法。 您也可以嘗試下列各項：

- [設定 TPM 證明。](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode)
- [ HGS 執行個體的 HTTPS。](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https)
- 開發可針對加密資料行發出豐富查詢的應用程式。
