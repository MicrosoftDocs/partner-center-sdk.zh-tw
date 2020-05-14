---
title: 更新自助式原則
description: 如何更新自助服務原則。
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d618d27dc7e17ff37b3186ad20fbc28057024538
ms.sourcegitcommit: 093dd5bb3e1a4d3d02839b39cec2b62d5800fd3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83383903"
---
# <a name="update-a-selfservepolicy"></a>更新 SelfServePolicy

**適用於：**

- 合作夥伴中心

本主題說明如何更新自助服務原則。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                       |
|----------|-------------------------------------------------------------------|
| **提出** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

- 需要要求識別碼和相互關聯識別碼。
- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>Request body

下表描述要求主體中的必要屬性。

| 名稱                              | 類型   | 描述                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| 物件 (object) | 自助服務原則資訊。 |

#### <a name="selfservepolicy"></a>SelfServePolicy

下表說明建立新的自助原則所需的[SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)資源所需的最低欄位。

| 屬性              | 類型             | 描述                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | 字串           | 成功建立自助原則時所提供的自助原則識別碼。     |
| SelfServeEntity       | SelfServeEntity  | 要授與存取權的自助實體。                                                     |
| 授與者               | 授與者          | 授與存取權的授與者。                                                                    |
| 權限           | 許可權陣列| [許可權](self-serve-policy-resources.md#permission)資源的陣列。                                                      |
| Etag                  | 字串           | Etag。                                                                                               |


### <a name="request-example"></a>要求範例

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此 API 會傳回已更新的自助原則的[SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼     | 錯誤碼   | 描述                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | 找不到自助服務原則                                            |
| 404                  | 600040       | 自助服務原則識別碼不正確                                  |


### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 Ok
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
