---
title: 變更計費擁週期
description: 將訂用帳戶更新為每月或每年計費。
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 9bd2545d4cf08f3bced1c5bc52b6c9fa1fa3c1df
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927393"
---
# <a name="change-the-billing-cycle"></a>變更計費擁週期

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

依每月計費或每年計費，更新 [訂單](order-resources.md) 。

在合作夥伴中心儀表板中，您可以藉由流覽至客戶的訂用帳戶詳細資料頁面來執行此操作。 一旦出現，您就會看到一個選項，定義訂用帳戶目前的計費週期，以及變更和提交的能力。

本文**涵蓋範圍外**：

- 變更試用的計費週期
- 變更任何非年度期限的計費週期，可 (每月、6年) & Azure 訂用帳戶
- 變更非使用中訂閱的計費週期
- 變更 Microsoft 線上服務授權型訂閱的計費週期

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在 [客戶帳戶] 頁面上，于 [**客戶帳戶資訊**] 區段中尋找**Microsoft ID** 。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 訂單識別碼。

## <a name="c"></a>C\#

若要變更計費週期的頻率，請更新 [**BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) 屬性。

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **補丁** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

下表列出變更訂用帳戶數量所需的查詢參數。

| 名稱                   | 類型 | 必要 | 描述                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **customer-tenant-id** | GUID |    Y     | 可識別客戶的 GUID 格式**客戶租使用者識別碼** |
| **訂單-識別碼**           | GUID |    Y     | 訂單識別碼                                                 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的屬性。

### <a name="order"></a>單

| 屬性           | 類型             | 必要 | 描述                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | 字串           |    N     | 成功建立訂單時提供的訂單識別碼 |
|>referencecustomerid | 字串           |    Y     | 客戶識別碼                                                    |
| BillingCycle       | 字串           |    Y     | 指出夥伴針對此訂單計費的頻率。 支援的值為在 [BillingCycleType](product-resources.md#billingcycletype) 中找到的成員名稱。 |
| LineItems          | 物件的陣列 |    Y     | [>orderlineitem](#orderlineitem)資源的陣列                      |
| CreationDate       | Datetime         |    N     | 訂單的建立日期（以日期時間格式）                        |
| 屬性         | 物件           |    N     | 包含 "ObjectType"： ">orderlineitem"                                     |

### <a name="orderlineitem"></a>OrderLineItem

| 屬性             | 類型   | 必要 | 描述                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | number |    Y     | 行專案編號，從0開始                                              |
| OfferId              | 字串 |    Y     | 供應專案的識別碼                                                                |
| SubscriptionId       | 字串 |    Y     | 訂用帳戶的識別碼                                                         |
| FriendlyName         | 字串 |    N     | 由合作夥伴定義之訂用帳戶的易記名稱，以協助區分 |
| 數量             | number |    Y     | 授權或實例的數目                                                |
| PartnerIdOnRecord    | 字串 |    N     | 記錄夥伴的 MPN 識別碼                                                |
| 屬性           | 物件 |    N     | 包含 "ObjectType"： ">orderlineitem"                                             |

### <a name="request-example"></a>要求範例

更新為年度帳單

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應本文中傳回更新的訂用帳戶訂單。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "Annual",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```