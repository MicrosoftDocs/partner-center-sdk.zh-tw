---
title: Get a list of offer categories by market
description: How to get a collection that contains all the offer categories in a given country/region and locale.
ms.assetid: 69174433-74C6-4294-ACAA-C2CE3D69CFEE
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: fd4f2b311d5bded4165c702510290360e9efdfaa
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487458"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>Get a list of offer categories by market

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

This topic describes how to get a collection that contains all the offer categories in a given country/region and locale.

## <a name="prerequisites"></a>必要條件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## <a name="c"></a>C\#

To get a list of offer categories in a given country/region and locale:

1. Use your [**IAggregatePartner.Operations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.
2. Inspect the [**OfferCategories**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

For an example, see the following:

- Sample: [Console test app](console-test-app.md)
- Project: **PartnerSDK.FeatureSample**
- Class: **PartnerSDK.FeatureSample**

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI 參數

This table lists the required query parameters to get the offer categories.

| 名稱           | 在工作列搜尋方塊中輸入       | 必要 | 說明            |
|----------------|------------|----------|------------------------|
| **country-id** | **string** | Y        | The country/region ID. |

### <a name="request-headers"></a>要求標頭

A **locale-id** formatted as a string is required.

See [Headers](headers.md) for more information.

### <a name="request-body"></a>要求主體

無。

### <a name="request-example"></a>要求的範例

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST response

If successful, this method returns a collection of **OfferCategory** resources in the response body.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For a full list, see [Error Codes](error-codes.md).

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
