---
title: REFRESH CUBE 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dafc13dda1f8ecab1400a88d1ca66eff5f317e43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63285075"
---
# <a name="mdx-data-definition---refresh-cube"></a>MDX 資料定義 - REFRESH CUBE


  重新整理 Cube 的用戶端快取。  
  
## <a name="syntax"></a>語法  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 用戶端應用程式連接到的執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，此陳述式會導致與伺服器同步處理用戶端應用程式快取的記憶體。 上述動作一般會自動偵測和更新，但發生前的時間長短相依於用戶端連接字串設定。 REFRESH CUBE 陳述式會立即重新整理資料。  
  
 對於連接到本機 Cube 的用戶端應用程式，REFRESH CUBE 陳述式會重建本機 Cube 檔案。  
  
> [!IMPORTANT]  
>  不會重新整理伺服器上儲存的命名集。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料定義陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
