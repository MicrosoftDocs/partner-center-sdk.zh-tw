---
title: 依識別碼取得 SKU
description: 使用指定的 SKU 識別碼，為指定的產品取得 SKU。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 33c8eb16c1327c8a92e48621d3f793c78aceaa19
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415652"
---
# <a name="get-a-sku-by-id"></a>依識別碼取得 SKU


**適用於**

- 夥伴中心

使用指定的 SKU 識別碼，為指定的產品取得 SKU。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 產品識別碼。 
- SKU 識別碼。 


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取得特定 SKU 的詳細資料，請先遵循[依識別碼取得產品](get-a-product-by-id.md)中的步驟來取得特定產品作業的介面。 從產生的介面中選取 [ **sku** ] 屬性，以取得具有適用于 sku 之可用作業的介面。 將 SKU 識別碼傳遞給**ById （）** 方法，並呼叫**Get （）** 或**GETASYNC （）** 以取得 SKU 詳細資料。

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId; 
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求語法**

| 方法  | 要求 URI                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}？ country = {國家/地區-代碼} HTTP/1。1   |

 

**URI 參數**

使用下列路徑和查詢參數，以使用指定的 SKU 識別碼來取得指定產品的 SKU。

| 名稱                   | 類型     | 必要項 | 描述                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 產品識別碼             | string   | 是      | 識別產品的字串。                           |
| sku-識別碼                 | string   | 是      | 識別 SKU 的字串。                               |
| 國家/地區代碼           | string   | 是      | 國家/地區識別碼。                                            |

 

**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應主體會包含[SKU](product-resources.md#sku)資源。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼     | 錯誤碼   | 描述                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | 找不到產品。                                                                                    |
| 404                  | 400018       | 找不到 Sku。                                                                                        |


**回應範例**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
    "minimumQuantity": 1,
    "maximumQuantity": 999999999,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "AzureSubscriptionRegistration",
        "InventoryCheck"
    ],
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
    }
}
```

