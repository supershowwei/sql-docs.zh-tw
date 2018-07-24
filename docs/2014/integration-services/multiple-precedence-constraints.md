---
title: 多個優先順序條件約束 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
caps.latest.revision: 44
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 60cd55a656849f3cb5eee9cac879a88d8d85ad4e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231453"
---
# <a name="multiple-precedence-constraints"></a>多個優先順序條件約束
  優先順序條件約束會連接兩個可執行檔：兩個工作、兩個容器，或一個工作和一個容器。 其稱為優先順序可執行檔與受條件約束的可執行檔。 條件約束可執行檔可包含多個優先順序條件約束。 如需詳細資訊，請參閱 [Precedence Constraints](control-flow/precedence-constraints.md)。  
  
 藉由群組條件約束來組裝複雜的條件約束案例，可讓您在封裝中實作複雜的控制流程。 例如，在下圖中，工作 D 連結到工作`Success`條件約束，工作 D 已連結到工作 B 所`Failure`條件約束，以及工作 D 連結到工作 C`Success`條件約束。 工作 D 與工作 A、工作 D 與工作 B，以及工作 D 與工作 C 之間的優先順序條件約束會參與邏輯 *and* 關聯性。 因此，工作 A 必須成功執行、工作 B 必須失敗，而且工作 C 必須成功執行，才可以執行工作 D。  
  
 ![優先順序條件約束所連結的工作](media/precedenceconstraints.gif "優先順序條件約束所連結的工作")  
  
## <a name="logicaland-property"></a>LogicalAnd 屬性  
 如果工作或容器具有多個條件約束，則 `LogicalAnd` 屬性會指定是只評估優先順序條件約束，還是同時評估其他條件約束。  
  
 您可以設定`LogicalAnd`屬性使用**優先順序條件約束編輯器**中[!INCLUDE[ssIS](../includes/ssis-md.md)]設計工具中，或在 [屬性] 視窗中，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]提供。  
  
## <a name="related-tasks"></a>相關工作  
 [設定優先順序條件約束的屬性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  