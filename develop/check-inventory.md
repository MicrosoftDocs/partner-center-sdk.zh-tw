---
title: 檢查清查
description: 檢查一組特定目錄專案的清查。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1dfd831917689f8d06dfb5b30b4d07a899f6eee0
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412908"
---
# <a name="check-inventory"></a>檢查清查

適用於：

- 夥伴中心

如何檢查一組特定目錄專案的清查。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 一或多個產品識別碼。 或者，也可以指定 SKU 識別碼。
- 驗證所提供的產品/SKU 識別碼所參考的 SKU 清查所需的任何其他內容。 這些需求可能因產品/SKU 類型而異，而且可以從[SKU 的](product-resources.md#sku) **InventoryVariables**屬性來判斷。 

## <a name="c"></a>C#


若要檢查清查，請針對每個要檢查的專案，使用[InventoryItem](product-resources.md#inventoryitem)物件來建立[InventoryCheckRequest](product-resources.md#inventorycheckrequest)物件。 然後，使用**Iaggregatepartner.customers.byid 擴充**功能存取子，將其範圍細分為**產品**，然後使用**ByCountry （）** 方法選取國家/地區。 最後，使用您的**InventoryCheckRequest**物件來呼叫**CheckInventory （）** 方法。

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/extensions/product/checkInventory？ country = {國家/地區-代碼} HTTP/1。1                        |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來檢查清查。

| 名稱                   | 類型     | 必要項 | 描述                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 國家/地區代碼           | string   | 是      | 國家/地區識別碼。                                            |

### <a name="request-headers"></a>要求標頭

- 如需詳細資訊，請參閱[標頭](headers.md)。

### <a name="request-body"></a>要求本文

清查要求詳細資料，由包含一或多個[InventoryItem](product-resources.md#inventoryitem)資源的[InventoryCheckRequest](product-resources.md#inventorycheckrequest)資源所組成。 

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="response"></a>回應

如果成功，回應主體會包含已填入限制詳細資料的[InventoryItem](product-resources.md#inventoryitem)物件集合（如果有的話）。

>[!NOTE]
>如果輸入 InventoryItem 代表在目錄中找不到的專案，它就不會包含在輸出集合中。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼     | 錯誤碼   | 描述                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 400                  | 2001         | 遺漏要求主體。                                                                              |
| 400                  | 400026       | 缺少必要的清查內容專案。                                                             |

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```