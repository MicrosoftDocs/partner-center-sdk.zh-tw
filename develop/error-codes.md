---
title: 合作夥伴中心 REST 錯誤碼
description: 來自合作夥伴中心 Api 的錯誤碼和成功回應的描述。
ms.date: 06/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b75f7fa6b9b82c2b1744a21fa0dbac95aa7c7acd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093997"
---
# <a name="partner-center-rest-error-codes"></a>合作夥伴中心 REST 錯誤碼

**適用於：**

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

| 名稱        | 類型   | 說明                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| code        | 字串 | 一律傳回。 表示所發生錯誤的類型。 非 Null。                                                                                  |
| description | 字串 | 一律傳回。 詳細說明錯誤，並提供其他偵錯資訊。 非 Null、非空白。 長度上限是 1024 個字元。 |
| data        | array  | 僅針對某些錯誤類型傳回。 錯誤物件的清單。                                                                                           |
| source      | 字串 | 一律傳回。 錯誤的來源。                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
}
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```
