---
title: 依訂單取得訂用帳戶清單
description: 取得對應至指定訂單的訂用帳戶資源集合。
ms.assetid: C6DCE351-8C02-42CD-9A80-8156BC6BF1B8
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 20bc7416059acd62caf940f976b4eddc3c3a0f23
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156920"
---
# <a name="get-a-list-of-subscriptions-by-order"></a>依訂單取得訂用帳戶清單

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得對應至指定訂單的[訂](subscription-resources.md)用帳戶資源集合。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 訂單識別碼。

## <a name="c"></a>C\#

若要依照訂單取得訂用帳戶清單，使用您的 **IAggregatePartner.Customers** 集合並呼叫 **ById()** 方法。 然後呼叫[**訂閱**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)屬性，後面接著**ByOrder （）** 方法。 藉由呼叫[**Get （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get)或[**GetAsync （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync)來完成。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSample**類別**： SubscriptionsByOrder.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions？訂單\_id = {ID-order} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

下表列出取得所有訂閱所需的查詢參數。

| 名稱                   | 類型     | 必要 | 描述                           |
|------------------------|----------|----------|---------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 對應至客戶的 GUID。 |
| **id-for-order**       | **guid** | Y        | 對應于訂單的 GUID。    |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳迴響應主體中的[訂](subscription-resources.md)用帳戶資源集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 25 Nov 2015 05:50:45 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "Myofferpurchase",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "{id-for-order}",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
