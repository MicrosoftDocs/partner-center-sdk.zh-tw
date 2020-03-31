---
title: 取得產品的 Sku 清單（依國家/地區）
description: 您可以使用合作夥伴中心 Api，依國家/地區針對產品取得及篩選 Sku 集合。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9613290c34cde57008247eeee05d71e99436d959
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416793"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a>取得產品的 Sku 清單（依國家/地區）

適用於：

- 夥伴中心

您可以使用合作夥伴中心 Api，取得特定產品的國家/地區所提供的 Sku 集合。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 產品識別碼。

## <a name="c"></a>C\#

若要取得產品的 Sku 清單：

1. 遵循依[識別碼取得產品](get-a-product-by-id.md)中的步驟，取得特定產品作業的介面。
2. 從介面中選取 [ **sku** ] 屬性，以取得具有適用于 sku 之可用作業的介面。
3. 呼叫**Get （）** 或**GetAsync （）** 方法，以取得產品的可用 sku 集合。
4. 選擇性使用**ByReservationScope （）** 方法選取保留範圍。
5. 選擇性在呼叫**Get （）** 或**GetAsync （）** 之前，請使用**ByTargetSegment （）** 方法依目標區段篩選 sku。

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

若要取得產品的 Sku 清單：

1. 遵循依[識別碼取得產品](get-a-product-by-id.md)中的步驟，取得特定產品作業的介面。
2. 從介面中選取**getSkus**函式，以取得具有適用于 sku 之可用作業的介面。
3. 呼叫**get （）** 函式，以取得產品的可用 sku 集合。
4. 選擇性在呼叫**get （）** 函式之前，請使用**byTargetSegment （）** 函數依目標區段篩選 sku。

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

若要取得產品的 Sku 清單：

1. 執行[**PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md)命令。
2. 選擇性指定**區段**參數，依目標區段篩選 sku。

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/products/{product-id}/skus？ country = {國家/地區-代碼} & targetSegment = {目標-區段} HTTP/1。1  |

##### <a name="uri-parameters"></a>URI 參數

使用下列路徑和查詢參數來取得產品的 Sku 清單。

| 名稱                   | 類型     | 必要項 | 描述                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 產品識別碼             | string   | 是      | 識別產品的字串。                           |
| 國家/地區代碼           | string   | 是      | 國家/地區識別碼。                                            |
| 目標-區段         | string   | 否       | 識別用於篩選之目標區段的字串。 |
| reservationScope | string   | 否 | 查詢 Azure 保留產品的 Sku 清單時，請指定 `reservationScope=AzurePlan` 來取得適用于 AzurePlan 的 Sku 清單。 排除此參數，以取得適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的 Azure 保留產品的 Sku 清單。  |

#### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

None。

#### <a name="request-examples"></a>要求範例

取得給定產品的 Sku 清單：

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

取得 Azure 保留產品的 Sku 清單。 只包含適用于 Azure 方案，而不是 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的 Sku：

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

取得 Azure 保留產品的 Sku 清單。 只包含適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶而非 Azure 方案的 Sku：

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

### <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[SKU](product-resources.md#sku)資源的集合。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼     | 錯誤碼   | 描述                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | 不允許存取要求的 targetSegment。                                                     |
| 404                  | 400013       | 找不到父產品。                                                                         |

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
