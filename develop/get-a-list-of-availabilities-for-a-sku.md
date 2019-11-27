---
title: 取得 SKU 的 hdinsight 清單（依國家/地區）
description: 如何取得指定產品和 SKU 的 hdinsight 集合（依客戶國家/地區）。
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
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>取得 SKU 的 hdinsight 清單（依國家/地區）

適用於：

- 合作夥伴中心

本主題描述如何針對指定的產品和 SKU，取得特定國家/地區的 hdinsight 集合。

## <a name="prerequisites"></a>必要條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 產品識別碼。
- SKU 識別碼。
- 國家/地區。

## <a name="c"></a>C\#

若要取得[SKU](product-resources.md#sku)的[hdinsight](product-resources.md#availability)清單：

1. 依照[依識別碼取得 SKU](get-a-sku-by-id.md)中的步驟來取得特定 SKU 作業的介面。
2. 從 SKU 介面中選取 [ **hdinsight** ] 屬性，以取得具有 hdinsight 作業的介面。
3. 選擇性使用**ByTargetSegment （）** 方法，依目標區段篩選 hdinsight。
4. 呼叫**Get （）** 或**GetAsync （）** ，以取得此 SKU 的 hdinsight 集合。

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

## <a name="rest"></a>停

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities？ country = {國家/地區-代碼} & targetSegment = {目標-區段} HTTP/1。1     |

#### <a name="uri-parameters"></a>URI 參數

使用下列路徑和查詢參數來取得 SKU 的 hdinsight 清單。

| 名稱                   | 類型     | 必要 | 描述                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 產品識別碼             | 字串   | 是      | 識別產品的字串。                           |
| sku-識別碼                 | 字串   | 是      | 識別 SKU 的字串。                               |
| 國家/地區代碼           | 字串   | 是      | 國家/地區識別碼。                                            |
| 目標-區段         | 字串   | 否       | 識別用於篩選之目標區段的字串。 |
| reservationScope | 字串   | 否 | 查詢 Azure 保留 SKU 的 hdinsight 清單時，請指定 `reservationScope=AzurePlan` 來取得適用于 AzurePlan 的 hdinsight 清單。 排除這個參數，以取得適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱的 hdinsight 清單。  |

#### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

無。

#### <a name="request-examples"></a>要求範例

##### <a name="availabilities-for-sku-by-country"></a>依國家/地區的 SKU hdinsight

遵循此範例來取得指定 SKU 的 hdinsight 清單（依國家/地區）：

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

##### <a name="availabilities-for-vm-reservations-azure-plan"></a>VM 保留的 hdinsight （Azure 方案）

遵循此範例來取得 Azure VM 保留 Sku 的 hdinsight 清單（依國家/地區）。 此範例適用于套用至 Azure 方案的 Sku：

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

##### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的 VM 保留 hdinsight

請遵循此範例來取得適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的 Azure VM 保留專案清單（依國家/地區）。

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

### <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[**可用性**](product-resources.md#availability)資源的集合。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼     | 錯誤碼   | 描述                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | 不允許存取要求的**targetSegment** 。                                                     |

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
