---
title: 升級所有目標伺服器，然後再升級主要伺服器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97272209c1ceba780711ecf4a07178ddf8943d49
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156721"
---
# <a name="upgrade-all-target-servers-before-upgrading-the-master-server"></a>先升級所有目標伺服器後再升級主要伺服器
  升級主要伺服器之前，請先升級所有設定為目標伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 若要在多伺服器環境中自動化管理，您至少必須有一個主要伺服器和一個目標伺服器。 主要伺服器會將作業散發到目標伺服器，並接收目標伺服器傳回的事件。 對於目標伺服器上執行的作業，主要伺服器也會儲存其作業定義的集中副本。  
  
 如果目前的伺服器設定為主要伺服器，請先升級所有目標伺服器，然後再升級主要伺服器。  
  
## <a name="corrective-action"></a>更正動作  
 如果您無法在升級主要伺服器之前升級所有目標伺服器，就必須在升級之後，脫離所有目標伺服器並重新編列它們。  
  
 如需詳細資訊，請參閱 「 自動化整個企業的管理，"的主題"How to:脫離目標伺服器從主要伺服器 」 和 「 如何：編列至主要目標伺服器 」 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
