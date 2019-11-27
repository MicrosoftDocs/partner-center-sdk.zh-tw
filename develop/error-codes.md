---
title: 合作夥伴中心 REST 錯誤碼
description: 來自合作夥伴中心 Api 的錯誤碼和成功回應的描述。
ms.assetid: 08AC1F2E-5847-4AD8-AE5B-0173C5DB589A
ms.date: 06/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7f9cb33c2518cef84d6948783da7d2c4337ecfaa
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489668"
---
# <a name="partner-center-rest-error-codes"></a>合作夥伴中心 REST 錯誤碼

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心 REST Api 會傳回包含狀態碼的 JSON 物件。 這段程式碼會指出您的要求是否成功或失敗。

## <a name="success-responses"></a>成功回應

**2xx**狀態碼指出已成功接收、瞭解及接受用戶端的要求。

## <a name="error-codes"></a>錯誤碼

下列**4xx**和**5xx**狀態碼表示錯誤：

- 400：不正確的要求
- 401：未經授權
- 403：禁止
- 404：找不到
- 405：不允許方法
- 406：不接受
- 409：衝突，錯誤碼
- 412：前置條件失敗
- 429：要求太多
- 500：內部伺服器錯誤
- 501：未執行
- 502：閘道不正確
- 503：服務無法使用
- 504：閘道超時

## <a name="error-responses"></a>錯誤回應

具有**4xx**或**5xx**狀態碼的任何回應都會包含錯誤訊息，其中包含有關所遇到錯誤狀況的其他詳細資料。

下表和程式碼範例描述錯誤回應的架構：

| 名稱        | 類型   | 描述                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| code        | 字串 | 一律傳回。 表示發生的錯誤類型。 非 null。                                                                                  |
| description | 字串 | 一律傳回。 詳細描述錯誤，並提供其他的調試資訊。 非 null、非空白。 長度上限為1024個字元。 |
| 資料        | 陣列  | 僅針對某些錯誤類型傳回。 錯誤物件的清單。                                                                                           |
| 來源      | 字串 | 一律傳回。 錯誤的來源。                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
## }
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```