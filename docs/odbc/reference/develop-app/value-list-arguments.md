---
title: 值清單引數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a971da68a8f2a35df8fa513e68d1eba127e9c430
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208558"
---
# <a name="value-list-arguments"></a>值清單引數
值清單引數是由要用來比對的逗號分隔值清單所組成。 ODBC 目錄函數中沒有只有一個值清單引數： *TableType*中的引數**SQLTables**。 設定*TableType*為 null 指標會與相同設 SQL_ALL_TABLE_TYPES，列舉值清單的所有可能的成員。 這個引數不會受到 SQL_ATTR_METADATA_ID 陳述式屬性。 如需詳細資訊，請參閱 < [SQLTables](../../../odbc/reference/syntax/sqltables-function.md)函式描述。
