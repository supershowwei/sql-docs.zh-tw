---
title: srv_willconvert (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_willconvert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e091dded3b9c763be6d5d891ac7026146feb0a0d
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246657"
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 決定 ODS 程式庫中是否提供特定資料類型轉換。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
```  
  
## <a name="arguments"></a>引數  
 *srctype*  
 表示要轉換之資料的資料類型。 此參數可以是任何擴充預存程序 API 資料類型。  
  
 *desttype*  
 表示轉換來源資料的目標資料類型。 此參數可以是任何擴充預存程序 API 資料類型。  
  
## <a name="returns"></a>傳回值  
 支援資料類型轉換時為 TRUE；不支援資料類型轉換時則為 FALSE。  
  
## <a name="remarks"></a>Remarks  
 如需每種資料類型的描述，請參閱[資料類型 &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://www.microsoft.com/en-us/msrc?rtc=1)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_convert &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
