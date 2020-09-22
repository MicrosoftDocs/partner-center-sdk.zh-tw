---
title: 建立訂單
description: 如何建立客戶的訂單。
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eb4dcea0f07ac759e2fa1f9ccd91f58f680ee535
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927355"
---
# <a name="create-an-order"></a>建立訂單

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**為 Azure 保留的 VM 實例產品建立訂單***僅*適用于：

- 合作夥伴中心

如需目前可供銷售之專案的相關資訊，請參閱 [雲端解決方案提供者計畫中的合作夥伴供應專案](/partner-center/csp-offers)。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 供應專案識別碼。

## <a name="c"></a>C\#

若要建立客戶的訂單：

1. 具現化 [**Order**](order-resources.md) 物件，並將 **>referencecustomerid** 屬性設定為客戶識別碼以記錄客戶。

2. 建立 [**>orderlineitem**](order-resources.md#orderlineitem) 物件的清單，並將清單指派給 Order 的 **LineItems** 屬性。 每個訂單明細項目都包含一個供應項目的購買資訊。 您必須有至少一個訂單明細項目。

3. 取得排序作業的介面。 首先，請使用客戶識別碼呼叫 [**>iaggregatepartner.customers >iaggregatepartner.customers.byid**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法，以識別客戶。 接下來，從 [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) 屬性取出介面。

4. 呼叫 [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) 或 [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) 方法，並傳入 [**Order**](order-resources.md) 物件。

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： CreateOrder.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

使用下列路徑參數來識別客戶。

| 名稱        | 類型   | 必要 | 描述                                                |
|-------------|--------|----------|------------------------------------------------------------|
| customer-id | 字串 | Yes      | 可識別客戶的 GUID 格式化客戶識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

#### <a name="order"></a>單

下表描述要求主體中的 [順序](order-resources.md) 屬性。

| 屬性             | 類型                        | 必要                        | 描述                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | 字串                      | No                              | 成功建立訂單時提供的訂單識別碼。   |
| referenceCustomerId  | 字串                      | No                              | 客戶識別碼。 |
| billingCycle         | 字串                      | No                              | 指出夥伴針對此訂單計費的頻率。 支援的值為在 [BillingCycleType](product-resources.md#billingcycletype) 中找到的成員名稱。 預設值為「每月」或「OneTime」（依順序建立）。 此欄位會在成功建立訂單時套用。 |
| lineItems            | [>orderlineitem](order-resources.md#orderlineitem)資源的陣列 | Yes      | 客戶所購買供應專案的詳細清單，包括數量。        |
| currencyCode         | 字串                      | No                              | 唯讀。 放置訂單時使用的貨幣。 在成功建立訂單時套用。           |
| creationDate         | Datetime                    | No                              | 唯讀。 訂單的建立日期 (採用日期-時間格式)。 在成功建立訂單時套用。                                   |
| status               | 字串                      | No                              | 唯讀。 訂單的狀態。  支援的值是在 [OrderStatus](order-resources.md#orderstatus)中找到的成員名稱。        |
| 連結                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | 對應至訂單的資源連結。 |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | No                              | 對應至順序的中繼資料屬性。 |

#### <a name="orderlineitem"></a>OrderLineItem

下表描述要求主體中的 [>orderlineitem](order-resources.md#orderlineitem) 屬性。

>[!NOTE]
>只有當間接提供者代表間接轉銷商放置訂單時，才應該提供 partnerIdOnRecord。 它只會用來儲存間接轉銷商的 Microsoft 合作夥伴網路識別碼， (永遠不會) 間接提供者的識別碼。

| 名稱                 | 類型   | 必要 | 描述                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Yes      | 集合中的每個明細項目都會取得唯一的行號 (從 0 數到 count-1)。                                                                                                                                                 |
| offerId              | 字串 | Yes      | 供應項目識別碼。                                                                                                                                                                                                                      |
| subscriptionId       | 字串 | No       | 訂用帳戶識別碼。                                                                                                                                                                                                               |
| parentSubscriptionId | 字串 | No       | 選擇性。 附加供應項目中父訂用帳戶的識別碼。 僅適用於 PATCH。                                                                                                                                                     |
| friendlyName         | 字串 | No       | 選擇性。 由夥伴定義之訂用帳戶的易記名稱，以協助區分。                                                                                                                                              |
| quantity             | int    | Yes      | 授權型訂用帳戶的授權數目。                                                                                                                                                                                   |
| partnerIdOnRecord    | 字串 | No       | 當間接提供者代表間接轉銷商進行訂單時，請使用 **間接轉銷** 商的 MPN 識別碼填入此欄位， (永遠不會) 間接提供者的識別碼。 這可確保適度的獎勵。 |
| provisioningCoNtext  | 字典<字串，字串>                | No       |  針對目錄中的某些專案布建所需的資訊。 SKU 中的 provisioningVariables 屬性會指出目錄中的特定專案需要哪些屬性。                  |
| 連結                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | No       |  唯讀。 對應至訂單明細專案的資源連結。  |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | No       | 對應至 >orderlineitem 的中繼資料屬性。 |
| renewsTo             | 物件的陣列                          | No    |[RenewsTo](order-resources.md#renewsto)資源的陣列。                                                                            |

##### <a name="renewsto"></a>RenewsTo

下表描述要求主體中的 [RenewsTo](order-resources.md#renewsto) 屬性。

| 屬性              | 類型             | 必要        | 描述 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | 字串           | No              | 續訂期限的持續時間的 ISO 8601 標記法。 目前支援的值會 **P1M** (1 個月) ，而 **P1Y** (1 年) 。 |

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>REST 回應

如果成功，方法會在回應主體中傳回 [訂單](order-resources.md) 資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
