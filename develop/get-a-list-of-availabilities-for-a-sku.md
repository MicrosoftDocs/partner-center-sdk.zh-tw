---
title: Get a list of availabilities for a SKU (by country)
description: How to get a collection of availabilities for the specified product and SKU by customer country.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2c761e97d0a9302c9b42947552b67464d6a0b64f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487528"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Get a list of availabilities for a SKU (by country)

適用於：

- 合作夥伴中心

This topic describes how to get a collection of availabilities in a particular country for a specified product and SKU.

## <a name="prerequisites"></a>必要條件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A product identifier.
- A SKU identifier.
- A country.

## <a name="c"></a>C\#

To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):

1. Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.
2. From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.
3. (Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.
4. Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST request

#### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1     |

#### <a name="uri-parameters"></a>URI 參數

Use the following path and query parameters to get a list of availabilities for a SKU.

| 名稱                   | 在工作列搜尋方塊中輸入     | 必要 | 說明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| product-id             | 字串   | [是]      | A string that identifies the product.                           |
| sku-id                 | 字串   | [是]      | A string that identifies the SKU.                               |
| country-code           | 字串   | [是]      | A country/region ID.                                            |
| target-segment         | 字串   | 無       | A string that identifies the target segment used for filtering. |
| reservationScope | 字串   | 無 | When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities which are applicable to AzurePlan. Exclude this parameter to get a list of availabilities which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.  |

#### <a name="request-headers"></a>要求標頭

For more information, see [Headers](headers.md).

#### <a name="request-body"></a>要求主體

無。

#### <a name="request-examples"></a>要求範例

##### <a name="availabilities-for-sku-by-country"></a>Availabilities for SKU by country

Follow this example to get a list of availabilities for a given SKU by country:

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

##### <a name="availabilities-for-vm-reservations-azure-plan"></a>Availabilities for VM reservations (Azure plan)

Follow this example to get a list of availabilities by country for Azure VM reservation SKUs. This example is for SKUs that apply to Azure plans:

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

##### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions

Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

### <a name="rest-response"></a>REST response

If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.

#### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For a full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP 狀態碼     | 錯誤碼   | 說明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Access to the requested **targetSegment** is not allowed.                                                     |

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
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
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
