---
title: HEX (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hexadecimal data
- HEX function
ms.assetid: f5d471ee-aeef-421c-b6e1-55b9676c3842
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 72e5b5982e8128169cfdc2431227d410be409b23
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217768"
---
# <a name="hex-ssis-expression"></a>HEX (SSIS 運算式)
  傳回代表整數的十六進位值的字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
HEX(integer_expression)  
```  
  
## <a name="arguments"></a>引數  
 *integer_expression*  
 是帶正負號或不帶正負號的整數。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 如果 *integer_expression* 是 Null，則 HEX 會傳回 Null。  
  
 *integer_expression* 引數必須評估為整數。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
 傳回結果不包含限定詞，例如 0x 前置詞。 若要包含前置詞，請使用 + (串連) 運算子。 如需詳細資訊，請參閱 [+ &#40;串連&#41; &#40;SSIS 運算式&#41;](concatenate-ssis-expression.md)。  
  
 HEX 標記法中使用的字母 A – F 會以大寫字元顯示。  
  
 整數資料類型的結果字串長度如下：  
  
-   DT_I1 和 DT_UI1 傳回最大長度為 2 的字串。  
  
-   DT_I2 和 DT_UI2 傳回最大長度為 4 的字串。  
  
-   DT_I4 和 DT_UI4 傳回最大長度為 8 的字串。  
  
-   DT_I8 和 DT_UI8 傳回最大長度為 16 的字串。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例使用數值常值。 函數傳回值 190。  
  
```  
HEX(400)   
```  
  
 此範例使用 **ReorderPoint** 資料行。 資料行資料類型為 `smallint`。 如果 **ReorderPoint** 是 750，則函數會傳回 2EE。  
  
```  
HEX(ReorderPoint)   
```  
  
 此範例使用系統變數 **LocaleID**。 如果 **LocaleID** 是 1033，則函數會傳回 409。  
  
```  
HEX(@LocaleID)  
```  
  
## <a name="see-also"></a>另請參閱  
 [函式&#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  