---
title: CERT_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERT_ID
- CERT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], certificates
- CERT_ID function
- IDs [SQL Server], certificates
- certificates [SQL Server], IDs
ms.assetid: 59cc06f5-272e-4936-8afe-afba7aba8eea
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b424d7c19f668d17dbe899804c2ef3002775a27
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708596"
---
# <a name="certid-transact-sql"></a>CERT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函式會傳回憑證的識別碼值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
Cert_ID ( 'cert_name' )  
```  
  
## <a name="arguments"></a>引數  
**'** *cert_name* **'**  

資料庫中憑證的名稱。
  
## <a name="return-types"></a>傳回類型
 **int**  
  
## <a name="remarks"></a>Remarks  
[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 目錄檢視會顯示憑證名稱。
  
## <a name="permissions"></a>[權限]  
需要憑證的適當權限，並且需要呼叫端尚未拒絕憑證的 VIEW DEFINITION 權限。 如需憑證權限的詳細資訊，請參閱 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md#permissions)。
  
## <a name="examples"></a>範例  
此範例會傳回名為 `ABerglundCert3` 之憑證的識別碼。
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  
