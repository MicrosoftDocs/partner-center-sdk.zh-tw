---
title: 取得 Microsoft Azure 定價
description: 如何使用 Azure 供應專案的即時價格取得 Azure 費率卡片。 Azure 定價是相當動態的，經常變動。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba7cbe1d58f997afe0a4fd0de929bc69debb65c1
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927013"
---
# <a name="get-prices-for-microsoft-azure"></a>取得 Microsoft Azure 定價

**適用於**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何使用 Azure 供應專案的即時價格取得 [Azure 費率卡片](azure-rate-card-resources.md) 。 Azure 定價是相當動態的，經常變動。

若要追蹤使用量並協助預測個別客戶的每月帳單和帳單，您可以結合此 Azure 費率卡片查詢來取得 Microsoft Azure 的價格，以 [取得客戶的 Azure 使用量記錄](get-a-customer-s-utilization-record-for-azure.md)。

價格會因市場與貨幣而異，而此 API 會將位置列入考慮。 根據預設，API 會在合作夥伴中心和您的瀏覽器語言中使用您的夥伴設定檔設定，而這些設定是可自訂的。 如果您從單一的集中式辦公室管理多個市場的銷售，則位置感知特別相關。 如需詳細資訊，請參閱 [URI 參數](#uri-parameters)。

## <a name="c"></a>C\#

若要取得 Azure 費率卡片，請呼叫 [**IAzureRateCard. 取得**/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) 方法，以傳回包含 Azure 價格的 [**>azureratecard**/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) 資源。

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： GetAzureRateCard.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要取得 Azure 費率卡片，請呼叫 **IAzureRateCard** 函式以傳回包含 azure 價格的費率卡片詳細資料。

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

若要取得 Azure 卡片，請執行 [**PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) 命令以傳回包含 azure 價格的費率卡片詳細資料。

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                        |
|---------|--------------------------------------------------------------------|
| **GET** | *{baseURL}*/v1/ratecards/azure？ currency = {currency} &區域 = {region} |

### <a name="uri-parameters"></a>URI 參數

| 名稱     | 類型   | 必要 | 描述                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 貨幣 | 字串 | No       | 選擇性的三個字母 ISO 代碼，適用于將提供資源費率的貨幣 (例如 `EUR`) 。 預設值為 `USD`。 |
| region   | 字串 | No       | 選擇性兩個字母的 ISO 國家/地區代碼，表示購買供應專案的市場 (例如 `FR`) 。 預設值為 `US`。        |

您可以在要求中包含選用的 X 地區設定 [標頭](headers.md#rest-request-headers) 。 如果您未包含 X 地區設定標頭，則會使用預設值 ( "en-us" ) 。

- 如果您在要求中提供貨幣和區域參數，則會使用 X 地區設定的值來判斷回應的語言。

- 如果您未在要求中提供區域和貨幣參數，則會使用 X 地區設定的值來決定回應的區域、貨幣和語言。

### <a name="request-header"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果要求成功，它會傳回 [Azure 費率卡片](azure-rate-card-resources.md) 資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en-US",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
