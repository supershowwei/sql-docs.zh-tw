---
title: 產生鏡像資料表和 CDC 擷取執行個體 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- mirTab
ms.assetid: 260c1617-eecc-4007-a84d-3c5778ce46b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 848de74437835311c8585001f5906169aa1dbb7f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771354"
---
# <a name="generate-mirror-tables-and-cdc-capture-instances"></a>產生鏡像資料表和 CDC 擷取執行個體
  使用 [產生鏡像資料表] 頁面，針對 CDC 執行個體中包含的資料表產生鏡像資料表。  
  
 按一下 **[執行]** ，建立鏡像資料表。 隨即顯示每一個資料表的建立進度，而且會顯示一則訊息，讓您知道每一個鏡像資料表是否已順利完成還是發生錯誤。 如果出現任何錯誤，請按一下 **[詳細資料]** ，查看包含錯誤說明的對話方塊。  
  
 如果有任何資料表建立失敗，您可以選擇繼續或刪除任何失敗的資料表，然後再繼續進行。 當精靈執行完之後，您可以決定是否要在 Oracle 來源資料庫中修正資料表，或者不要在 CDC 執行個體中使用此資料表。 如果您修正此資料表，當您 [Edit Tables](edit-tables.md)時可以將它加入。  
  
 按 **[下一步]** ，開啟 [Finish](finish.md) 頁面。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](how-to-create-the-sql-server-change-database-instance.md)  
  
  
