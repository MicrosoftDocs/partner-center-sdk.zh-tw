---
title: 依識別碼取得可用性
description: 使用可用性識別碼取得指定產品和 SKU 的可用性。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093895"
---
# <a name="get-the-availability-by-id"></a>依識別碼取得可用性

**適用於**

- 合作夥伴中心

使用可用性識別碼取得指定產品和 SKU 的可用性。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 產品識別碼。

- SKU 識別碼。

- 可用性識別碼。

## <a name="c"></a>C\#

若要取得特定[可用性](product-resources.md#availability)的詳細資料，請從使用[依識別碼取得 SKU](get-a-sku-by-id.md)中的步驟開始，以取得特定[SKU](product-resources.md#sku)作業的介面。 從產生的介面中選取 [ **hdinsight** ] 屬性，以取得具有 hdinsight 可用作業的介面。 之後，請將可用性識別碼傳遞給**ById （）** 方法，以取得該特定可用性的作業，然後呼叫**get （）** 或**GetAsync （）** 以取得可用性詳細資料。

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要取得特定[可用性](product-resources.md#availability)的詳細資料，請從使用[依識別碼取得 SKU](get-a-sku-by-id.md)中的步驟開始，以取得特定[SKU](product-resources.md#sku)作業的介面。 從產生的介面中選取**getAvailabilities**函式，以取得具有 hdinsight 可用作業的介面。 之後，請將可用性識別碼傳遞給**byId （）** 函式，以取得該特定可用性的作業，然後呼叫**get （）** 函式來取得可用性詳細資料。

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

若要取得特定[可用性](product-resources.md#availability)的詳細資料，請執行[**PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) ，並指定**AvailabilityId**、 **CountryCode**、 **ProductId**和**SkuId**參數，以取得可用性詳細資料。

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}？ country = {國家/地區-代碼} HTTP/1。1         |

### <a name="uri-parameter"></a>URI 參數

使用下列路徑和查詢參數，以使用可用性識別碼來取得特定的可用性。

| 名稱                   | 類型     | 必要 | 說明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 產品識別碼             | 字串   | Yes      | 識別產品的 GUID 格式字串。            |
| sku-識別碼                 | 字串   | Yes      | 識別 SKU 的 GUID 格式字串。                |
| 可用性-識別碼        | 字串   | Yes      | 識別可用性的 GUID 格式字串。       |
| 國家/地區代碼           | 字串   | Yes      | 國家/地區識別碼。                                            |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[可用性](product-resources.md#availability)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼     | 錯誤碼   | 描述                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | 找不到產品。                                                                                    |
| 404                  | 400018       | 找不到 Sku。                                                                                        |
| 404                  | 400019       | 找不到可用性。                                                                                   |

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": false,
    "terms": [{
        "duration": "P1Y",
        "description": "1 Year Prepaid"
    }],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
