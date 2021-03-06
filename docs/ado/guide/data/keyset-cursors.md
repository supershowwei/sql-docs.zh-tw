---
title: 索引鍵集資料指標 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2ff246d01254ceb2b526b5118553d72cc499046
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161639"
---
# <a name="keyset-cursors"></a>索引鍵集資料指標
索引鍵集資料指標偵測變更的能力提供靜態和動態資料指標之間的功能。 如同靜態資料指標，它不一定會偵測結果集的成員資格和順序變更。 如同動態資料指標，它會偵測結果集中的資料列值變更。  
  
 索引鍵集驅動資料指標是由稱為索引鍵集的一組唯一識別碼 (索引鍵) 所控制。 索引鍵是從結果集中唯一識別資料列的一組資料行建立的。 索引鍵集是一組取自由查詢陳述式傳回之所有資料列的索引鍵值。  
  
 使用索引鍵集驅動資料指標，會在資料指標中為每個資料列建置和保留一個索引鍵，並儲存在用戶端工作站或伺服器上。 當您存取每個資料列時，會使用此預存金鑰從資料來源擷取目前的資料值。 在索引鍵集驅動資料指標中，當完整擴展索引鍵集時，結果集的成員資格會遭到凍結。 之後，在重新開啟之前，都不會在結果集中新增或更新受影響的成員資格。  
  
 當使用者捲動結果集，會顯示資料值 （索引鍵集擁有者或其他處理序） 的變更。 只有在關閉並重新開啟資料指標之後，才能看見其他處理序在資料指標外部執行的插入。 在結果集結尾可看見從資料指標內部執行的插入。  
  
 索引鍵集驅動資料指標的嘗試擷取已刪除的資料列，資料列會顯示為結果集內的 「 漏洞 」。 索引鍵集中存在資料列的索引鍵，但結果集中不再有此資料列。 如果已更新資料列中的索引鍵值，資料列視為已刪除，然後插入，因此這類資料列也會顯示為結果集中的漏洞。 雖然索引鍵集驅動資料指標一律可以偵測其他程序所刪除的資料列，它可以選擇性地移除它本身進行刪除的資料列的索引鍵。 執行這項操作的索引鍵集驅動資料指標無法偵測到自己刪除，因為已移除的辨識項。  
  
 索引鍵資料行的更新的運作方式類似 刪除舊的索引鍵後面插入新的金鑰。 無法更新不是透過資料指標時才會看見新的金鑰值。 透過資料指標進行更新，新的索引鍵值可見的結果集的結尾。  
  
 沒有稱為索引鍵集導向的標準資料指標的索引鍵集驅動資料指標的變化。 中索引鍵集導向的標準資料指標，結果集中的資料列的成員資格和資料列的順序固定在資料指標開啟時，但變更會藉由資料指標擁有者的值，其他處理序認可的變更會顯示。 如果變更 disqualifies 成員資格的資料列，或會影響資料列的順序，資料列就不會消失或移動，除非資料指標已關閉並重新開啟。 插入的資料不會出現，但是現有的資料變更就會出現，因為不擷取資料列。  
  
 索引鍵集驅動資料指標很難正確使用因為資料變更的敏感性取決於許多不同的情況下，如上面所述。 不過，如果您的應用程式不會關心並行更新，可以以程式設計方式處理不正確的索引鍵，而且必須直接存取特定索引鍵的資料列，索引鍵集驅動資料指標可能適合您。 使用  **adOpenKeyset CursorTypeEnum**來指出您想要使用在 ADO 中索引鍵集資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)   
 [靜態資料指標](../../../ado/guide/data/static-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
