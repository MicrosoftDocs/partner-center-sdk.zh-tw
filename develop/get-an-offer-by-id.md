---
title: 依照識別碼取得供應項目
description: 取得符合供應專案識別碼的供應專案資源。
ms.assetid: F5165C5A-7C93-4F8E-A733-641511BC8FB7
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0b3cb5856bb9b4259267c2284d8b00668f4427cf
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157750"
---
# <a name="get-an-offer-by-id"></a>依照識別碼取得供應項目

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得符合供應專案識別碼的**供應**專案資源。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 供應專案識別碼。

## <a name="c"></a>C\#

若要依識別碼尋找特定的供應專案，請使用您的**iaggregatepartner.customers.byid**集合、透過呼叫**ByCountry （）** 建立國家/地區，然後呼叫[**ByID （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid)方法。 然後，呼叫[**get （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get)或[**get Async （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync)方法。

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSample**類別**： GetOffer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要依識別碼尋找特定供應專案，請使用**iaggregatepartner.customers.byid. getOffers**函式，並呼叫**byCountry （）** 函數來建立國家/地區，然後呼叫**byID （）** 函式。 然後呼叫**get （）** 函數。

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

若要依識別碼尋找特定的供應專案，請執行[**PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md)命令，並指定**CountryCode**和**OfferId**參數。

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id} 嗎？國家/地區 = {country-ID} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

| 名稱           | 類型       | 必要 | 描述                           |
|----------------|------------|----------|---------------------------------------|
| **供應專案識別碼**   | **guid**   | Y        | 可對應至供應項目的 GUID。 |
| **country-id** | **string** | Y        | 國家/地區識別碼。                |

### <a name="request-headers"></a>要求標頭

- 需要格式化為字串的**地區設定識別碼**。
如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**供應**專案資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Mon, 23 Nov 2015 23:13:01 GMT

{
    "id": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "name": "Office 365 Business Premium",
    "description": "For businesses with 1 to 300 users that need the latest desktop version of Office,
                    plus anywhere access to email, filesharing, and online conferencing.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "rank": 56,
    "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/031C9E47-4802-4248-838E-778FB1D2CC05",
    "locale": "en-us",
    "country": "US",
    "category": {
        "id": "SmallBusiness_Key",
        "name": "Small Business",
        "rank": 30,
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
    "product": {
        "id": "f245ecc8-75af-4f8e-b61f-27d8114de5f3",
        "name": "Office 365 Business Premium",
        "unit": "Licenses"
    },
    "unitType": "Licenses",
    "links": {
        "learnMore": {
            "uri": "http: //g.microsoftonline.com/0BXPS00en/909",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Offer"
    }
}
```
