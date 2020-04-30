---
title: 依照識別碼取得產品
description: 使用產品識別碼取得指定的產品資源。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d3a6a7714e318f0b9c23bbd59098d0a0188d8c20
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155470"
---
# <a name="get-a-product-by-id"></a>依照識別碼取得產品

**適用于**

- 合作夥伴中心

使用產品識別碼取得指定的產品資源。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 產品識別碼。

## <a name="c"></a>C\#

若要依識別碼尋找特定產品，請使用您的**iaggregatepartner.customers.byid**集合，然後使用**ByCountry （）** 方法來選取國家/地區，再呼叫**ById （）** 方法。 最後，呼叫**Get （）** 或**GetAsync （）** 方法，以傳回產品。

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

若要依識別碼尋找特定產品，請使用您的**iaggregatepartner.customers.byid. getProducts**函式，使用**byCountry （）** 函式來選取國家/地區，然後呼叫**byId （）** 函數。 最後，呼叫**get （）** 函數來傳回產品。

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

若要依識別碼尋找特定產品，請執行[**PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)命令，並指定**ProductId**參數。 **CountryCode**參數是選項，如果未指定，則會使用與轉售商相關聯的國家/地區。

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}？ country = {COUNTRY} HTTP/1。1  |

### <a name="uri-parameter"></a>URI 參數

使用下列路徑參數來取得指定的產品。

| 名稱                   | 類型     | 必要 | 描述                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 產品識別碼             | 字串   | 是      | 識別產品的字串。                           |
| country                | 字串   | 是      | 國家/地區識別碼。                                            |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[產品](product-resources.md#product)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼     | 錯誤碼   | 描述                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 400013       | 找不到產品。                                                     |

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
