---
title: 取得訂用帳戶的附加元件清單
description: 如何取得客戶已選擇要新增至其訂用帳戶的附加元件集合。
ms.assetid: F10823A2-CA77-4F80-9ED4-CFB4E4343049
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6b10fd79c1e93ebc8d888c72433fe2ee86f48bbf
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416227"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a>取得訂用帳戶的附加元件清單

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本主題描述如何取得客戶已選擇要新增至其 **[訂](subscription-resources.md)** 用帳戶資源的附加元件集合。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（**客戶租使用者識別碼**）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- 訂用帳戶識別碼。

## <a name="c"></a>C\#

若要取得客戶訂用帳戶的附加元件清單：

1. 使用您的**iaggregatepartner.customers.byid. Customers**集合來呼叫**ById （）** 方法。
2. 呼叫[**訂閱**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)屬性，後面接著[**ById （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)方法。
3. 呼叫[**附加元件**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons)屬性，後面接著[**Get （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get)或[**GetAsync （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync)。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();


```

如需範例，請參閱下列各項：

- 範例：[主控台測試應用程式](console-test-app.md)
- 專案： **PartnerSDK. FeatureSample**
- 類別： **SubscriptionAddons.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

下表列出必要的查詢參數，以取得訂用帳戶的附加元件清單。

| 名稱                    | 類型     | 必要項 | 描述                               |
|-------------------------|----------|----------|-------------------------------------------|
| **客戶-租使用者識別碼**  | **guid** | Y        | 對應至客戶的 GUID。     |
| **訂用帳戶的識別碼** | **guid** | Y        | 對應至訂用帳戶的 GUID。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

### <a name="request-body"></a>要求本文

None。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳迴響應主體中的資源集合。

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
        "entitlementId": "42226ed6-070a-4e0f-b80c-4cdfB3e97aa7",
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
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
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
