---
title: 錯誤訊息 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b38734544ac3accb3ddfdbcae8ae92f67b252e54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62805852"
---
# <a name="error-messages"></a>錯誤訊息
  所傳回的訊息文字[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會置於*MessageText*參數**SQLGetDiagRec**。 錯誤的來源會由訊息的標頭指出：  
  
 [Microsoft][ODBC Driver Manager]  
 這些錯誤是由 ODBC 驅動程式管理員所引發。  
  
 [Microsoft][ODBC Cursor Library]  
 這些錯誤是由 ODBC 資料指標程式庫所引發。  
  
 [Microsoft][SQL Server Native Client]  
 這些錯誤所引發[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式。 如果沒有具有 Net-Library 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱的任何其他節點，則驅動程式會發生錯誤。  
  
 [Microsoft][SQL Server Native Client][*Net-Transportname*]  
 這些錯誤所引發[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]網路程式庫，其中*Net-transportname*顯示名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（比方說，具名管道、 共用記憶體、 TCP/IP 通訊端或 VIA） 的用戶端的網路傳輸。 錯誤訊息的其餘部份則包含呼叫的 Net-Library 函數，以及由 TDS 函數在基礎網路 API 中所呼叫的函數。 *PfNative*傳回這些錯誤的錯誤程式碼為基礎的網路通訊協定堆疊的錯誤程式碼。  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 這些錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所引發。 錯誤訊息的其餘部分是來自於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的錯誤訊息文字。 *PfNative*傳回這些錯誤的程式碼是錯誤號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需有關可以傳回的錯誤訊息 （和其數字） 清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱的描述和錯誤資料行**sysmessages**中的系統資料表**主要**資料庫中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  
