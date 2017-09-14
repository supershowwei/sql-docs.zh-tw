---
title: "DTAXML 元素 (DTA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- DTAXML element
ms.assetid: 3d9942ed-8a27-40db-a7c9-808984d914a2
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 175cfd247df19129f39d1e4ed8914da32dd57d11
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="dtaxml-element-dta"></a>DTAXML 元素 (DTA)
  Database Engine Tuning Advisor XML 輸入或輸出檔的根元素， **DTAXML** 包含說明 Database Engine Tuning Advisor 所產生之微調輸入和微調輸出的所有元素。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAXML   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/dta">  
    ...code removed here...  
</DTAXML>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|Attribute|描述|  
|---------------|-----------------|  
|**xmlns:xsi**|必要。 識別 XML 結構描述執行個體命名空間。 這個命名空間的屬性用來參考驗證 Database Engine Tuning Advisor XML 檔時所用的結構描述。<br /><br /> 必要值： [http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)|  
|**xmlns**|必要。 識別 Database Engine Tuning Advisor 命名空間。<br /><br /> 如果您利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 XML 編輯器來編輯 Database Engine Tuning Advisor，[F1 說明和動態說明] 便會利用這個值，在《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中，尋找可能的參考主題。<br /><br /> 必要值：<br /><br /> [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?LinkId=43100) 命名空間|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 DTA XML 檔需要使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|無|  
|**子元素**|[DTAInput 元素 &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)<br /><br /> **DTAOutput** 元素 (相關資訊請參閱 [Database Engine Tuning Advisor XML 結構描述](http://schemas.microsoft.com/sqlserver/) )|  
  
## <a name="remarks"></a>備註  
 如需有關 XML 命名空間的詳細資訊，請參閱 [MSDN Library 中的＜](http://go.microsoft.com/fwlink/?LinkId=7341) XML 文件中的命名空間 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ＞(英文)。  
  
## <a name="example"></a>範例  
 如需一般 **DTAXML** 元素的範例，請參閱 [XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入的檔參考 &#40; Database Engine Tuning advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)   
 [啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)  
  
  