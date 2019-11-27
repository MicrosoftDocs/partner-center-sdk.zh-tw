---
title: 取得 SKU 的 hdinsight 清單（由客戶）
description: 您可以使用客戶、產品和 SKU 識別碼，針對指定的產品和 SKU 取得 hdinsight 集合。
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 33c65f49a0f0425e12e40e202a7b0a6cebb7def6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487478"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a>取得 SKU 的 hdinsight 清單（由客戶）

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用下列方法，針對特定客戶可用的指定產品和 SKU，取得 hdinsight 的集合。

## <a name="prerequisites"></a>先決條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（**客戶租使用者 id**）。
- 產品識別碼（**產品 id**）。
- SKU 識別碼（**sku-id**）。

## <a name="rest"></a>停

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1。1 |

#### <a name="request-uri-parameters"></a>要求 URI 參數

| 名字               | 類型 | 必要 | 說明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| 客戶-租使用者識別碼 | GUID | 是 | 值是 GUID 格式的**客戶租使用者**識別碼，這是可讓您指定客戶的識別碼。 |
| 產品識別碼 | string | 是 | 識別產品的字串。 |
| sku-識別碼 | string | 是 | 識別 SKU 的 string。 |

#### <a name="request-header"></a>要求標頭

- 如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

無。

#### <a name="request-example"></a>要求的範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

### <a name="rest-response"></a>REST 回應

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼 | 錯誤碼 | 說明 |
|------------------|------------|-------------|
| 404 | 400013 | 找不到父產品。 |

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Microsoft Azure plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
