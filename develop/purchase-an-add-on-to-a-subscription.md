---
title: 購買要加入訂用帳戶的附加元件
description: 如何購買現有訂用帳戶的附加元件。
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69c817cc89b97cea43533c170cef598df99095f7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096721"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>購買要加入訂用帳戶的附加元件

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何購買現有訂用帳戶的附加元件。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 訂用帳戶識別碼。 這是要購買附加元件供應專案的現有訂用帳戶。

- 識別要購買之附加元件的供應專案識別碼。

## <a name="purchasing-an-add-on-through-code"></a>透過程式碼購買附加元件

當您購買訂用帳戶的附加元件時，您會以附加元件的順序來更新原始訂閱順序。 在下列中，customerId 是客戶識別碼，subscriptionId 是訂用帳戶識別碼，而 addOnOfferId 是附加元件的供應專案識別碼。

以下是步驟：

1.  取得訂用帳戶作業的介面。

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  使用該介面來具現化訂用帳戶物件。 這會取得父訂用帳戶的詳細資料，包括訂單識別碼。

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  具現化新的[**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order)物件。 此訂單實例用來更新用來購買訂用帳戶的原始訂單。 將單行專案新增至代表附加元件的順序。
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  以附加元件的新訂單，更新訂用帳戶的原始訂單。
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

若要購買附加元件，請先呼叫[**iaggregatepartner.customers.byid 的 ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶，然後使用[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法來識別具有附加元件供應專案的訂用帳戶，以取得訂用帳戶作業的介面。 使用該[**介面**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription)，藉由呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)來抓取訂用帳戶詳細資料。 為什麼需要訂用帳戶的詳細資料？ 因為您需要訂用帳戶訂單的訂單識別碼。 這就是使用附加元件更新的順序。

接下來，將新的[**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order)物件具現化，並以包含用來識別附加元件資訊的單一[**LineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem)實例填入它，如下列程式碼片段所示。 您將使用這個新物件，以附加元件來更新訂閱順序。 最後，在第一次使用[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)客戶和訂單[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)之後，呼叫[**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch)方法來更新訂用帳戶訂單。

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： AddSubscriptionAddOn.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **跳** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

使用下列參數來識別客戶和訂單。

| 名稱                   | 類型     | 必要 | 說明                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 此值是可識別客戶的 GUID 格式**客戶租使用者識別碼**。 |
| **訂單識別碼**           | **guid** | Y        | 訂單識別碼。                                                              |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的屬性。

## <a name="order"></a>單

| 名稱                | 類型             | 必要 | 說明                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | 字串           | N        | 訂單識別碼。                                        |
| ReferenceCustomerId | 字串           | Y        | 客戶識別碼。                                     |
| LineItems           | 物件的陣列 | Y        | [OrderLineItem](#orderlineitem)物件的陣列。 |
| CreationDate        | 字串           | N        | 訂單的建立日期 (採用日期-時間格式)。 |
| 屬性          | 物件 (object)           | N        | 包含 "ObjectType"： "Order"。                      |

## <a name="orderlineitem"></a>OrderLineItem

| 名稱                 | 類型   | 必要 | 說明                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | number | Y        | 行專案編號，從0開始。                       |
| OfferId              | 字串 | Y        | 附加元件的供應專案識別碼。                                  |
| SubscriptionId       | 字串 | N        | 購買的附加元件訂用帳戶的識別碼。                 |
| ParentSubscriptionId | 字串 | Y        | 具有附加元件供應專案之父訂用帳戶的識別碼。 |
| FriendlyName         | 字串 | N        | 此行專案的易記名稱。                        |
| 數量             | number | Y        | 授權的數目。                                      |
| PartnerIdOnRecord    | 字串 | N        | 記錄夥伴的 MPN 識別碼。                         |
| 屬性           | 物件 (object) | N        | 包含 "ObjectType"： "OrderLineItem"。                      |

### <a name="request-example"></a>要求範例

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
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
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

如果成功，此方法會在回應主體中傳回更新的訂閱順序。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

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
    "billingCycle": "none",
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
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
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
