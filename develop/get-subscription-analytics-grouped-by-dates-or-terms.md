---
title: 取得依日期或詞彙分組的訂用帳戶分析
description: 如何取得依日期或詞彙分組的訂用帳戶分析資訊。
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097523"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>取得依日期或詞彙分組的訂用帳戶分析

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何取得客戶的訂用帳戶分析資訊，並依日期或詞彙分組。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI |
|--------|-------------|
| **GET** | [* \{ baseURL \} *](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions？ groupby = {groupby_queries} |

### <a name="uri-parameters"></a>URI 參數

使用下列必要的 path 參數來識別您的組織，並將結果分組。

| 名稱 | 類型 | 必要 | 描述 |
|------|------|----------|-------------|
| groupby_queries | 字串與日期時間的配對 | Yes | 用來篩選結果的詞彙和日期。 |

### <a name="groupby-syntax"></a>GroupBy 語法

Group by 參數必須以一系列以逗號分隔的域值來組成。

未編碼的範例如下所示：

```http
?groupby=termField1,dateField1,termField2
```

下表顯示 [群組依據] 支援的欄位清單。

| 欄位 | 類型 | Description |
|-------|------|-------------|
| customerTenantId | 字串 | GUID 格式的字串，可識別客戶租使用者。 |
| customerName | 字串 | 客戶的名稱。 |
| customerMarket | 字串 | 客戶執行業務的國家/地區。 |
| id | 字串 | 用來識別訂用帳戶的 GUID 格式字串。 |
| status | 字串 | 訂用帳戶狀態。 支援的值為： "ACTIVE"、"暫止" 或 "取消布建"。 |
| productName | 字串 | 產品的名稱。 |
| subscriptionType | 字串 | 訂閱類型。 注意：此欄位會區分大小寫。 支援的值為： "Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS"。 |
| autoRenewEnabled | Boolean | 值，指出是否自動更新訂用帳戶。 |
| partnerId  | 字串 | MPN 識別碼。 若為直接轉銷商，此參數將會是合作夥伴的 MPN 識別碼。 若為間接轉銷商，此參數將會是間接轉銷商的 MPN 識別碼。 |
| friendlyName | 字串 | 訂閱的名稱。 |
| partnerName | 字串 | 購買訂閱之夥伴的名稱 |
| providerName | 字串 | 若為間接轉銷商的訂閱交易，提供者名稱就是購買訂閱的間接提供者。
| creationDate | UTC 日期時間格式的字串 | 建立訂用帳戶的日期。 |
| effectiveStartDate | UTC 日期時間格式的字串 | 訂用帳戶開始的日期。 |
| commitmentEndDate | UTC 日期時間格式的字串 | 訂閱結束的日期。 |
| currentStateEndDate | UTC 日期時間格式的字串 | 訂用帳戶的目前狀態將會變更的日期。 |
| trialToPaidConversionDate | UTC 日期時間格式的字串 | 訂用帳戶從試用版轉換成付費的日期。 預設值為 null。 |
| trialStartDate | UTC 日期時間格式的字串 | 訂用帳戶的試用期開始日期。 預設值為 null。 |
| lastUsageDate | UTC 日期時間格式的字串 | 上次使用訂用帳戶的日期。 預設值為 null。 |
| deprovisionedDate | UTC 日期時間格式的字串 | 取消布建訂用帳戶的日期。 預設值為 null。 |
| lastRenewalDate | UTC 日期時間格式的字串 | 上次更新訂用帳戶的日期。 預設值為 null。 |

### <a name="filter-fields"></a>篩選欄位

下表列出選擇性的篩選欄位和其描述：

| 欄位 | 類型 |  Description |
|-------|------|--------------|
| top | int | 在要求中傳回的資料列數目。 如果未指定值，則最大值和預設值為10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。 |
| skip | int | 在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 例如，top = 10000 和 skip = 0 會抓取前10000個數據列，top = 10000，skip = 10000 會抓取下一個10000個數據列。 |
| filter | 字串 | 一或多個篩選回應中資料列的陳述式。 每個篩選語句都會包含回應主體的功能變數名稱，以及與、或相關聯的值 **`eq`** ， **`ne`** 適用于特定欄位的 **`contains`** 運算子。 語句可以使用或結合 **`and`** **`or`** 。 篩選 參數中的字串值必須由單引號括住。 請參閱下一節，以取得可篩選的欄位清單，以及這些欄位支援的運算子。 |
| aggregationLevel | 字串 | 指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：**day**、**week** 或 **month**。 如果未指定值，則預設為**dateRange**。 **注意**：只有在將日期欄位當做 groupBy 參數的一部分傳遞時，此參數才適用。 |
| groupBy | 字串 | 將資料彙總僅套用至指定欄位的陳述式。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含依指定的詞彙和日期分組的[訂](partner-center-analytics-resources.md#subscription-resource)用帳戶資源集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a>另請參閱

[合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
