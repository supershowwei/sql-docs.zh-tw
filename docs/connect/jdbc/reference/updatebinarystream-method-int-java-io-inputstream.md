---
title: "updateBinaryStream 方法 （int，java.io.InputStream） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ede0acb87e477f965696521117c99d410bd0b19
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>updateBinaryStream 方法 (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用二進位資料流值，更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 **Int** ，指出資料行索引。  
  
 *x*  
  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateBinaryStream 方法 java.sql.ResultSet 介面中所指定此 updateBinaryStream 方法。  
  
 使用這個方法來**映像**，**文字**，和**ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別可能會影響效能。  
  
 這個方法會將位元組傳遞從 InputStream 物件選取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]例如 binary、 varbinary、 varbinary （max）、 影像、 xml 和 udt 的二進位資料行。 這個方法不支援更新字元資料行。 若要更新 InputStream 字元資料行，請使用[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)方法。  
  
## <a name="see-also"></a>另請參閱  
 [updateBinaryStream 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  