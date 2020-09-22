---
title: 使用附加元件建立購物車
description: 如何在購物車中加入客戶的附加元件訂單。
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: bea4f9059bf494cd30f7daabf349669433a0e291
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927574"
---
# <a name="create-a-cart-with-add-ons"></a>使用附加元件建立購物車

**適用於：**

- 合作夥伴中心

您可以透過購物車購買附加元件。 如需目前可供銷售之專案的詳細資訊，請參閱 [雲端解決方案提供者計畫中的合作夥伴供應專案](/partner-center/csp-offers)。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

## <a name="c"></a>C\#

購物車可讓您購買基礎供應專案及其對應的附加元件。 遵循下列步驟來建立購物車：

1. 將 [**購物車**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) 物件具現化。

2. 建立 [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) 物件的清單，這些物件代表 (s 的基底供應專案) ，並將清單指派給購物車的 [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) 屬性。

3. 在每個基底供應專案的購物車明細專案下，以其他**CartLineItem**物件填入**AddOnItems**清單，其中每個物件都代表將針對該基底供應專案購買的附加元件。

4. 使用 [**>iaggregatepartner.customers**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) 透過客戶識別碼呼叫 [**ICustomerCollection >iaggregatepartner.customers.byid**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法以識別客戶，然後從 **購物車** 屬性中取出介面，以取得購物車作業的介面。

5. 最後，呼叫 [**create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) 或 [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) 方法來建立購物車。

### <a name="c-example"></a>C \# 範例

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

遵循下列步驟來建立購物車，以針對現有的基本訂用帳戶 () ，購買附加元件 () ：

1. 使用新的**CartLineItem**建立**購物車**，其中包含**ProvisioningCoNtext**屬性中的訂用帳戶識別碼，其索引鍵為 "ParentSubscriptionId"。

2. 呼叫 **Create** 或 **CreateAsync** 方法。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1。1                        |

#### <a name="uri-parameter"></a>URI 參數

使用下列路徑參數來識別客戶。

| 名稱            | 類型     | 必要 | 描述                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **客戶識別碼** | 字串   | Yes      | 可識別客戶的 GUID 格式化客戶識別碼。             |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的 [購物車](cart-resources.md) 屬性。

| 屬性              | 類型             | 必要        | 描述 |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | 字串           | No              | 成功建立購物車時所提供的購物車識別碼。                                  |
| creationTimeStamp     | Datetime         | No              | 購物車的建立日期（以日期時間格式）。 在成功建立購物車時申請。         |
| lastModifiedTimeStamp | Datetime         | No              | 購物車上次更新的日期（以日期時間格式）。 在成功建立購物車時申請。    |
| expirationTimeStamp   | Datetime         | No              | 購物車將到期的日期（以日期時間格式）。  在成功建立購物車時申請。            |
| lastModifiedUser      | 字串           | No              | 上次更新購物車的使用者。 在成功建立購物車時申請。                             |
| lineItems             | 物件的陣列 | Yes             | [CartLineItem](cart-resources.md#cartlineitem)資源的陣列。                                             |

下表描述要求主體中的 [CartLineItem](cart-resources.md#cartlineitem) 屬性。

| 屬性             | 類型                             | 描述                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | 字串                           | 購物車明細專案的唯一識別碼。 在成功建立購物車時申請。                                                                   |
| catalogId            | 字串                           | 目錄專案識別碼。                                                                                                                          |
| friendlyName         | 字串                           | 選擇性。 由夥伴定義之專案的易記名稱，以協助區分。                                                                 |
| quantity             | int                              | 授權或實例的數目。                                                                                                                  |
| currencyCode         | 字串                           | 貨幣代碼。                                                                                                                                    |
| billingCycle         | 物件                           | 針對目前期間設定的計費週期類型。                                                                                                 |
| 參與者         | 物件字串組的清單      | PartnerId on Record 的集合，會在購買時) 記錄 (MPNID。                                                                                          |
| provisioningCoNtext  | 字典<字串，字串>       | 用於布建供應專案的內容。                                                                                                             |
| orderGroup           | 字串                           | 用來指出哪些專案可以放在一起的群組。                                                                                               |
| addonItems           | **CartLineItem**物件的清單 | 附加元件的購物車明細專案集合，將會針對由父購物車明細專案購買所產生的基本訂用帳戶購買。 |
| error                | 物件                           | 如果發生錯誤，就會在購物車建立之後套用。                                                                                                    |

### <a name="request-example-new-base-subscription"></a> (新的基本訂用帳戶) 的要求範例

下列 REST 範例示範如何使用新的基底訂用帳戶的附加元件專案來建立購物車。

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a> (現有的基本訂用帳戶) 的要求範例

下列 REST 範例示範如何將附加元件附加至現有的基底訂用帳戶。

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回已填入的 [購物車](cart-resources.md) 資源。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

#### <a name="response-example-new-base-subscription"></a> (新的基本訂用帳戶) 的回應範例

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a> (現有的基本訂用帳戶) 的回應範例

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
