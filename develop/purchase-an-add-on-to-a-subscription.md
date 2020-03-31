---
title: 購買訂用帳戶的附加元件
description: 如何購買現有訂用帳戶的附加元件。
ms.assetid: 743520E5-0501-4403-B977-5E6D3E32DEC3
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f49685eb142945fc94e551e2113799c4c5b959e5
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416311"
---
# <a name="span-idpc_apiv2purchase_an_add-on_to_a_subscriptionpurchase-an-add-on-to-a-subscription"></a><span id="pc_apiv2.purchase_an_add-on_to_a_subscription"/>購買訂用帳戶的附加元件


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何購買現有訂用帳戶的附加元件。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- 訂用帳戶識別碼。 這是要購買附加元件供應專案的現有訂用帳戶。
- 識別要購買之附加元件的供應專案識別碼。

## <a name="span-idpurchasing_an_add-on_through_codespan-idpurchasing_an_add-on_through_codespan-idpurchasing_an_add-on_through_codepurchasing-an-add-on-through-code"></a><span id="Purchasing_an_add-on_through_code"/><span id="purchasing_an_add-on_through_code"/><span id="PURCHASING_AN_ADD-ON_THROUGH_CODE"/>透過程式碼購買附加元件


當您購買訂用帳戶的附加元件時，您會以附加元件的順序來更新原始訂閱順序。 在下列中，customerId 是客戶識別碼，subscriptionId 是訂用帳戶識別碼，而 addOnOfferId 是附加元件的供應專案識別碼。

步驟如下：

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

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


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

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法    | 要求 URI                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **跳** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1。1 |

 

**URI 參數**

使用下列參數來識別客戶和訂單。

| 名稱                   | 類型     | 必要項 | 描述                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 此值是可識別客戶的 GUID 格式**客戶租使用者識別碼**。 |
| **訂單識別碼**           | **guid** | Y        | 訂單識別碼。                                                              |

 

**要求標頭**

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

下表描述要求主體中的屬性。

## <a name="span-idorderspan-idorderspan-idorderorder"></a><span id="Order"/><span id="order"/><span id="ORDER"/>順序


| 名稱                | 類型             | 必要項 | 描述                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | string           | N        | 訂單識別碼。                                        |
| referenceCustomerId | string           | Y        | 客戶識別碼。                                     |
| lineItems           | 物件的陣列 | Y        | [OrderLineItem](#orderlineitem)物件的陣列。 |
| CreationDate        | string           | N        | 訂單的建立日期（採用日期時間格式）。 |
| 屬性          | object           | N        | 包含 "ObjectType"： "Order"。                      |

 

## <a name="span-idorderlineitemspan-idorderlineitemspan-idorderlineitemorderlineitem"></a><span id="orderLineItem"/><span id="orderlineitem"/><span id="ORDERLINEITEM"/>OrderLineItem


| 名稱                 | 類型   | 必要項 | 描述                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| lineItemNumber       | 數字 | Y        | 行專案編號，從0開始。                       |
| OfferId              | string | Y        | 附加元件的供應專案識別碼。                                  |
| SubscriptionId       | string | N        | 購買的附加元件訂用帳戶的識別碼。                 |
| parentSubscriptionId | string | Y        | 具有附加元件供應專案之父訂用帳戶的識別碼。 |
| FriendlyName         | string | N        | 此行專案的易記名稱。                        |
| 數量             | 數字 | Y        | 授權的數目。                                      |
| partnerIdOnRecord    | string | N        | 記錄夥伴的 MPN 識別碼。                         |
| 屬性           | object | N        | 包含 "ObjectType"： "OrderLineItem"。                      |

 

**要求範例**

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

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，此方法會在回應主體中傳回更新的訂閱順序。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

**回應範例**

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

 

 




