---
title: 轉換訂用帳戶
description: 將客戶的訂用帳戶升級為指定的目標訂用帳戶。
ms.assetid: 54618BC1-6AF7-4518-925B-8A6A4C926CE7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 936d01c608e26d02d14934d1b585c7b142ff0186
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157650"
---
# <a name="transition-a-subscription"></a>轉換訂用帳戶

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

將客戶的訂用帳戶升級為指定的目標訂用帳戶。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 兩個訂用帳戶識別碼，一個用於初始訂用帳戶，另一個用於目標訂用帳戶。

## <a name="c"></a>C\#

若要升級客戶的訂用帳戶，請先[取得 customer's 訂](get-a-subscription-by-id.md)用帳戶。 然後，藉由呼叫**升級**屬性，後面接著**Get （）** 或**GetAsync （）** 方法，取得該訂用帳戶的升級清單。 從該升級清單中選擇目標升級，然後呼叫初始訂用帳戶的**升級**屬性，後面接著**Create （）** 方法。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionIdForUpgrade;
// Upgrade targetOffer;

UpgradeResult upgradeResult = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionIdForUpgrade).Upgrades.Create(targetOffer);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSamples**類別**： UpgradeSubscription.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1。1 |
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1。1       |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來轉換訂用帳戶。

| 名稱                    | 類型     | 必要 | 描述                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **customer-tenant-id**  | **guid** | Y        | 對應至客戶的 GUID。             |
| **id-for-subscription** | **guid** | Y        | 對應至初始訂用帳戶的 GUID。 |
| **識別碼-目標**       | **guid** | Y        | 對應到目標訂用帳戶的 GUID。  |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

None

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

POST https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
Content-Type: application/json
Content-Length: 1098
Expect: 100-continue

{
    "TargetOffer":{
        "Id":"796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Name":"Office 365 Enterprise E3",
        "Description":"The best plan for businesses that need full productivity, communication and collaboration tools with the familiar Office suite, including Office Online.",
        "MinimumQuantity":1,
        "MaximumQuantity":10000000,
        "Rank":61,
        "Uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Locale":"en-us",
        "Country":"US",
        "Category":{
            "Id":"Enterprise_Key",
            "Name":"Enterprise",
            "Rank":20,
            "Locale":"en-us",
            "Country":"US",
            "Attributes":{
                "ObjectType":"OfferCategory"
            }
        },
        "PrerequisiteOffers":[],
        "IsAddOn":false,
        "IsAvailableForPurchase":true,
        "Billing":"license",
        "IsAutoRenewable":true,
        "Product":{
            "Id":"6fd2c87f-b296-42f0-b197-1e91e994b900",
            "Name":"Office 365 Enterprise E3",
            "Unit":"Licenses"
        },
        "UnitType":"Licenses",
        "Links":{
            "LearnMore":{
                "Uri":"http://g.microsoftonline.com/0BXPS00en/1015",
                "Method":"GET",
                "Headers":[]
            }
        }
        "Attributes":{
            "ObjectType":"Offer"
        }
    },
    "UpgradeType":1,
    "IsEligible":true,
    "Quantity":1,
    "UpgradeErrors":[],
    "Attributes":{
        "ObjectType":"Upgrade"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**升級**結果資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 29 Jan 2016 20:42:26 GMT

{
    "totalCount": 1,
    "items": [{
        "targetOffer": {
            "id": "91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "name": "Office 365 Enterprise E1",
            "description": "For businesses that need communication and collaboration tools and the ability to read and do lightweight editing of documents with Office Online.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 48,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "locale": "en-us",
            "country": "US",
            "category": {
                "id": "Enterprise_Key",
                "name": "Enterprise",
                "rank": 20,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": [],
            "isAddOn": false,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "isInternal": false,
            "conversionTargetOffers": [],
            "partnerQualifications": ["none"],
            "product": {
                "id": "18181a46-0d4e-45cd-891e-60aabd171b4e",
                "name": "Office 365 Enterprise E1",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "uri": "http://g.microsoftonline.com/0BXPS00en/1013",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/91FD106F-4B2C-4938-95AC-F54F74E9A239?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        },
        "upgradeType": "upgrade_only",
        "isEligible": false,
        "quantity": 1,
        "upgradeErrors": [{
            "code": 2,
            "description": "Subscription cannot be upgraded because the source subscription state is not active.  Additional Details contains the current source subscription state.",
            "attributes": {
                "objectType": "UpgradeError"
            }
        }],
        "attributes": {
            "objectType": "Upgrade"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}

HTTP/1.1 200 OK
Content-Length: 448
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CV: RnK86LBbDkWP/w2R.0
MS-ServerId: 102031201
Date: Fri, 29 Jan 2016 20:44:21 GMT

{
    "sourceSubscriptionId":"896a2862-67e2-4f3d-bb3f-c50c42b5fad8",
    "targetSubscriptionId":"2add8a55-454a-4ae5-a4c9-5107dc6e9768",
    "upgradeType":1,
    "upgradeErrors":[],
    "licenseErrors":[],
    "attributes":{
        "objectType":"UpgradeResult"
    }
}
```
