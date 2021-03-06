---
title: 確保有足夠的 TempDB 空間 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67dc3f6bb82799382fa2b65754b3645dd735acab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214813"
---
# <a name="ensuring-sufficient-tempdb-space"></a>確認 TempDB 有足夠空間
如果在處理時所發生的錯誤[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)需要處理在 Microsoft SQL Server 6.5 的空間的物件，您可能需要增加 TempDB 的大小。 (某些查詢需要暫存處理空間; 例如，具有 ORDER BY 子句的查詢需要排序的**資料錄集**，這需要一些暫存空間。)  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!IMPORTANT]
>  閱讀此程序之前執行的動作，因為它不縮小裝置之後它會展開, 一樣簡單。  
  
> [!NOTE]
>  根據預設的 Microsoft SQL Server 7.0 和更新版本、 TempDB 是設定為視需要自動成長。 因此，此程序可能只必須執行早於 7.0 版本的伺服器上。  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>若要增加 SQL Server 6.5 的 TempDB 空間  
  
1.  啟動 Microsoft SQL Server Enterprise Manager、 開啟樹狀結構的伺服器，然後再開啟資料庫裝置的樹狀結構。  
  
2.  選取 （實體） 的裝置，若要擴充，例如 Master，然後按兩下要開啟的裝置**編輯資料庫裝置** 對話方塊。  
  
     此對話方塊會顯示目前的資料庫使用的空間量。  
  
3.  在 **大小**方塊中，增加裝置所需的數量 (例如，50 mb (MB) 的硬碟空間)。  
  
4.  按一下 **立即變更**增加，可以展開 （邏輯） 的 TempDB 的空間數量。  
  
5.  開啟資料庫樹狀目錄中的伺服器上，，然後按兩下**TempDB**來開啟**編輯資料庫** 對話方塊。 **資料庫**索引標籤會列出目前配置給 TempDB 的空間數量 (**的資料大小**)。 根據預設，這會是 2 MB。  
  
6.  底下**大小**群組中，按一下**展開**。 圖形顯示每個實體裝置的可用和已配置的空間。 色彩暗紅色橫條代表可用空間。  
  
7.  選取 [**記錄檔裝置**，例如 Master，以顯示可用的大小，以**大小 (MB)** ] 方塊中。  
  
8.  按一下 **現在展開**酃 TempDB 資料庫。  
  
     **編輯資料庫**對話方塊會顯示新針對 TempDB 配置大小。  
  
 如需有關本主題的詳細資訊，請搜尋 「 展開資料庫對話方塊。 」 的 Microsoft SQL Server Enterprise Manager 的說明檔  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


