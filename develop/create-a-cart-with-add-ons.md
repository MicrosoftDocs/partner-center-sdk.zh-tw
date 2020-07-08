---
title: 使用附加元件建立購物車
description: 如何為購物車中的客戶新增訂單和附加元件。
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 6528c83b64908d08f058f18a987c5b7362312551
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096293"
---
# <a name="create-a-cart-with-add-ons"></a>使用附加元件建立購物車

**適用於：**

- 合作夥伴中心

您可以透過購物車購買附加元件。 如需目前可用來銷售之專案的詳細資訊，請參閱[雲端解決方案提供者方案中的合作夥伴優惠](https://docs.microsoft.com/partner-center/csp-offers)。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

## <a name="c"></a>C\#

購物車可讓您購買基底供應專案及其對應的附加元件。 請遵循下列步驟來建立購物車：

1. 具現化[**購物車**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cart)物件。

2. 建立代表基底供應專案的[**CartLineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem)物件清單，並將清單指派給購物車的[**LineItems**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)屬性。

3. 在每個基底供應專案的 [購物車] 明細專案底下，將**AddOnItems**清單填入其他**CartLineItem**物件，這些物件分別代表會針對該基底供應專案購買的附加元件。

4. 藉由使用[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner)呼叫[**ICustomerCollection. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶，然後從**購物車**屬性取得介面，以取得購物車作業的介面。

5. 最後，呼叫[**create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync)方法來建立購物車。

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

請遵循下列步驟來建立可讓您針對現有的基本訂用帳戶購買附加元件的購物車：

1. 建立具有新**CartLineItem**的**購物車**，其中包含**ProvisioningCoNtext**屬性中索引鍵為 "PARENTSUBSCRIPTIONID" 的訂用帳戶識別碼。

2. 呼叫**Create**或**CreateAsync**方法。

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
| **客戶識別碼** | 字串   | Yes      | 識別客戶的 GUID 格式客戶識別碼。             |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的[購物車](cart-resources.md)屬性。

| 屬性              | 類型             | 必要        | 描述 |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | 字串           | No              | 成功建立購物車時所提供的購物車識別碼。                                  |
| creationTimeStamp     | Datetime         | No              | 購物車的建立日期（以日期時間格式）。 已在成功建立購物車時套用。         |
| lastModifiedTimeStamp | Datetime         | No              | 購物車上次更新的日期（以日期時間格式）。 已在成功建立購物車時套用。    |
| expirationTimeStamp   | Datetime         | No              | 購物車將到期的日期，以日期時間格式為限。  已在成功建立購物車時申請。            |
| lastModifiedUser      | 字串           | No              | 上次更新購物車的使用者。 已在成功建立購物車時申請。                             |
| lineItems             | 物件的陣列 | Yes             | [CartLineItem](cart-resources.md#cartlineitem)資源的陣列。                                             |

下表描述要求主體中的[CartLineItem](cart-resources.md#cartlineitem)屬性。

| 屬性             | 類型                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | 字串                           | 購物車明細專案的唯一識別碼。 已在成功建立購物車時申請。                                                                   |
| catalogId            | 字串                           | 目錄專案識別碼。                                                                                                                          |
| friendlyName         | 字串                           | 選擇性。 由夥伴定義以協助區分的專案易記名稱。                                                                 |
| quantity             | int                              | 授權或實例的數目。                                                                                                                  |
| currencyCode         | 字串                           | 貨幣代碼。                                                                                                                                    |
| billingCycle         | Object                           | 針對目前期間所設定的計費週期類型。                                                                                                 |
| 參與者         | 物件字串配對的清單      | 在購買時，記錄（MPNID）上的 PartnerId 集合。                                                                                          |
| provisioningCoNtext  | 字典<字串，字串>       | 用於布建供應專案的內容。                                                                                                             |
| orderGroup           | 字串                           | 用來指出哪些專案可以放在一起的群組。                                                                                               |
| addonItems           | **CartLineItem**物件的清單 | 附加元件的購物車明細專案集合，將會向「父購物車」明細專案購買結果的「基本」訂用帳戶購買。 |
| 錯誤                | Object                           | 在購物車建立後，發生錯誤時套用。                                                                                                    |

### <a name="request-example-new-base-subscription"></a>要求範例（新的基本訂用帳戶）

下列 REST 範例示範如何使用新的基本訂用帳戶的附加元件來建立購物車。

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

#### <a name="request-example-existing-base-subscription"></a>要求範例（現有的基本訂用帳戶）

下列 REST 範例示範如何將附加元件附加至現有的基本訂用帳戶。

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

如果成功，此方法會在回應本文中傳回已填入的[購物車](cart-resources.md)資源。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

#### <a name="response-example-new-base-subscription"></a>回應範例（新的基本訂用帳戶）

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

#### <a name="response-example-existing-base-subscription"></a>回應範例（現有的基本訂用帳戶）

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
