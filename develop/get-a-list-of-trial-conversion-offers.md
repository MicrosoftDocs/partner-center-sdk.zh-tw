---
title: 取得試用版轉換方案的清單
description: 如何取得試用版轉換供應專案清單。
ms.assetid: 7B97505F-10B9-4ACD-9307-111FC1E7D042
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e55edde2753f3c6ec7e85db9f4463072e09a8cd4
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156910"
---
# <a name="get-a-list-of-trial-conversion-offers"></a>取得試用版轉換方案的清單

**適用于**

- 合作夥伴中心

如何取得試用版轉換供應專案清單。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 有效試用訂用帳戶的訂用帳戶識別碼。

## <a name="c"></a>C\#

若要取得可用試用轉換的清單，請從使用[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來開始，以識別客戶。 然後，使用試用版訂用帳戶識別碼呼叫[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法，以取得訂用帳戶作業的介面。 接下來，使用 [[**轉換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions)] 屬性來取得轉換上可用作業的介面，然後呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync)方法，以取得可用[**轉換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)供應專案的集合。

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列路徑參數來識別客戶和試用版訂用帳戶。

| 名稱            | 類型   | 必要 | 描述                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| customer-id     | 字串 | 是      | 識別客戶的 GUID 格式字串。           |
| subscription-id | 字串 | 是      | 可識別試用訂閱的 GUID 格式字串。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[轉換](conversions-resources.md#conversionresult)資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 305
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CV: feJByqU1X0ObaTQr.0
MS-ServerId: 030011719
Date: Thu, 15 Jun 2017 23:10:01 GMT

 {
    "totalCount": 1,
    "items": [{
            "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
            "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
            "orderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
            "quantity": 25,
            "billingCycle": "monthly",
            "attributes": {
                "objectType": "Conversion"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
