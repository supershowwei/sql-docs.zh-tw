---
title: updateBoolean 方法 (java.lang.String, boolean) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBoolean (java.lang.String, boolean)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5fed9ebb-d9a3-4d1a-9212-1057a603c4e5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7218cd8f86fa6fe65f6820c77b54f77654dce7b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667356"
---
# <a name="updateboolean-method-javalangstring-boolean"></a>updateBoolean 方法 (java.lang.String, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的資料行名稱，使用 **boolean** 值來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBoolean(java.lang.String columnName,  
                          boolean x)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 包含資料行名稱的**字串**。  
  
 *x*  
  
 **boolean** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 updateBoolean 方法是由 java.sql.ResultSet 介面中的 updateBoolean 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [updateBoolean 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
