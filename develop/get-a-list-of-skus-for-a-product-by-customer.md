---
title: 取得產品的 Sku 清單（由客戶）
description: 取得客戶所指定產品的 Sku 集合。
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: fb149389e9da11ea8e03d869eebbf9c96e83504e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412738"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a>取得產品的 Sku 清單（由客戶）

**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得可供現有客戶使用之特定產品的 Sku 集合。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼 (**customer-tenant-id**)。
- 產品識別碼（**產品識別碼**）。

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1。1 |

#### <a name="request-uri-parameter"></a>要求 URI 參數

| 名稱               | 類型 | 必要項 | 描述                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | 是 | 此值是 GUID 格式的 **customer-tenant-id**，此識別碼可讓您用來指定客戶。 |
| 產品識別碼 | string | 是 | 識別產品的字串。 |

#### <a name="request-header"></a>要求的標頭

- 如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

None。

#### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

### <a name="rest-response"></a>REST 回應

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼 | 錯誤碼 | 描述 |
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
    "id": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Gain access to Azure Services.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "Azure",
            "displayName": "Azure"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BPS6/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "localizedAttributes": [
        {
            "key": "OfferType",
            "value": "OfferType"
        },
        {
            "key": "Standard",
            "value": "Standard"
        },
        {
            "key": "DevTest",
            "value": "Dev/Test"
        }
    ]
}
```
