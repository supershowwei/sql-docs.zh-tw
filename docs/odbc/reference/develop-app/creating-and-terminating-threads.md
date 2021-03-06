---
title: 建立及終止執行緒 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9d6d15c449d88043e844addd12ac10a98d5c4a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470866"
---
# <a name="creating-and-terminating-threads"></a>建立及終止執行緒
使用 ODBC 的多執行緒應用程式應該呼叫 Microsoft® Visual C++® 執行階段程式庫函式 **_beginthread**並 **_endthread** (或是 **_beginthreadex**並 **_endthreadex**) 來建立和終止呼叫 ODBC 驅動程式管理員的執行緒。 如果應用程式呼叫 Microsoft Windows NT® 函式**CreateThread**並**EndThread**相反地，記憶體會發生外洩，因為驅動程式管理員和某些 ODBC 驅動程式呼叫 C 執行階段函式建立藉由呼叫的執行緒上將無法運作**CreateThread**。 如需詳細資訊，請參閱 Microsoft Windows® 文件。
