---
title: GetCurrentCertificate 方法 （ServerSettings 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- GetCurrentCertificate Method (ServerSettings Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 450e33c6-91d4-420f-ab7c-1905111f5658
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 30b704d26d2b6ac080f32034bb78fddcee446bdb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62736124"
---
# <a name="getcurrentcertificate-method-serversettings-class"></a>GetCurrentCertificate 方法 (ServerSettings 類別)
  取得目前的安全性憑證。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.GetCurrentCertificate(  
SHA  
)  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示 `ServerSettings` 執行個體上之伺服器設定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*SHA*|在方法完成之後指定目前安全性憑證的字串物件值 (輸出參數)。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
