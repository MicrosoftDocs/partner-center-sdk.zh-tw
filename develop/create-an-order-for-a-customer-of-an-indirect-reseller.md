---
title: 為間接轉銷商的客戶建立訂單
description: 如何為間接轉銷商的客戶建立訂單。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 880d626e6a7f4317575af8978348768e555a226e
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926684"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>為間接轉銷商的客戶建立訂單

**適用於：**

- 合作夥伴中心

如何為間接轉銷商的客戶建立訂單。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 要購買之專案的供應專案識別碼。

- 間接轉銷商的租使用者識別碼。

## <a name="c"></a>C\#

為間接轉銷商的客戶建立訂單：

1. 取得間接轉銷商的集合，這些轉銷商與已登入的合作夥伴有關聯性。

2. 取得集合中符合間接轉銷商識別碼之專案的本機變數。 當您建立訂單時，此步驟可協助您存取轉售商的 [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) 屬性。

3. 具現化 [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) 物件，並將 [**>referencecustomerid**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) 屬性設定為客戶識別碼，以便記錄客戶。

4. 建立 [**>orderlineitem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) 物件的清單，並將清單指派給 Order 的 [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) 屬性。 每個訂單明細項目都包含一個供應項目的購買資訊。 請務必在具有間接轉銷商 MPN 識別碼的每個明細專案中填入 [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) 屬性。 您必須有至少一個訂單明細項目。

5. 藉由呼叫 [**>iaggregatepartner.customers 的 >iaggregatepartner.customers.byid**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法與客戶識別碼來識別客戶，然後從 [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) 屬性取得介面，以取得排序作業的介面。

6. 呼叫 [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) 或 [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) 方法來建立訂單。

### <a name="c-example"></a>C \# 範例

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**範例**： [主控台測試應用程式](console-test-app.md)**專案**：合作夥伴中心 SDK 範例 **類別**： PlaceOrderForCustomer.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

使用下列路徑參數來識別客戶。

| 名稱        | 類型   | 必要 | 描述                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | 字串 | Yes      | 可識別客戶的 GUID 格式字串。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

#### <a name="order"></a>單

下表描述要求主體中的 **順序** 屬性。

| 名稱 | 類型 | 必要 | 描述 |
| ---- | ---- | -------- | ----------- |
| id | 字串 | No | 成功建立訂單時提供的訂單識別碼。 |
| referenceCustomerId | 字串 | Yes | 客戶識別碼。 |
| billingCycle | 字串 | No | 針對這張訂單向合作夥伴計費的頻率。 預設值為 [ &quot; 每月] &quot; ，並且會在成功建立訂單時套用。 支援的值是在 [**>billingcycletype**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)中找到的成員名稱。 注意：年度帳單功能尚未正式推出。 即將推出年度計費的支援。 |
| lineItems | 物件的陣列 | Yes | [**>orderlineitem**](#orderlineitem)資源的陣列。 |
| creationDate | 字串 | No | 訂單的建立日期 (採用日期-時間格式)。 在成功建立訂單時套用。 |
| 屬性 | 物件 (object) | No | 包含 "ObjectType"： "Order"。 |

#### <a name="orderlineitem"></a>OrderLineItem

下表描述要求主體中的 **>orderlineitem** 屬性。

| 名稱 | 類型 | 必要 | 描述 |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Yes | 集合中的每個明細項目都會取得唯一的行號 (從 0 數到 count-1)。 |
| offerId | 字串 | Yes | 供應項目識別碼。 |
| subscriptionId | 字串 | No | 訂用帳戶識別碼。 |
| parentSubscriptionId | 字串 | No | 選擇性。 附加供應項目中父訂用帳戶的識別碼。 僅適用於 PATCH。 |
| friendlyName | 字串 | No | 選擇性。 由夥伴定義之訂用帳戶的易記名稱，以協助區分。 |
| quantity | int | Yes | 授權型訂用帳戶的授權數目。 |
| partnerIdOnRecord | 字串 | No | 當間接提供者代表間接轉銷商進行訂單時，請使用 **間接轉銷** 商的 MPN 識別碼填入此欄位， (永遠不會) 間接提供者的識別碼。 這可確保適度的獎勵。 **無法提供轉售商 MPN 識別碼並不會導致訂單失敗。不過，轉銷商不會被記錄，因此結果獎勵計算可能不會包含銷售。** |
| 屬性 | 物件 (object) | No | 包含 "ObjectType"： ">orderlineitem"。 |

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
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

如果成功，回應主體會包含已填入的 [訂單](order-resources.md) 資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
