---
title: 透過搜尋查詢取得訂用帳戶分析
description: 如何取得搜尋查詢所篩選的訂用帳戶分析資訊。
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097551"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>取得根據搜尋查詢所篩選的訂用帳戶分析資訊

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何為您的客戶取得搜尋查詢所篩選的訂用帳戶分析資訊。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI |
|--------|-------------|
| **GET** | [* \{ baseURL \} *](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions？ filter = {filter_string} |

### <a name="uri-parameters"></a>URI 參數

使用下列必要的 path 參數來識別您的組織並篩選搜尋。

| 名稱 | 類型 | 必要 | 說明 |
|------|------|----------|-------------|
| filter_string | 字串 | Yes | 要套用至訂用帳戶分析的篩選準則。 請參閱篩選語法和篩選欄位章節，以瞭解要在此參數中使用的語法、欄位和運算子。 |

### <a name="filter-syntax"></a>篩選語法

篩選參數必須以一系列的欄位、值和運算子組合來組成。 可以使用 or 運算子來合併多個組合 **`and`** **`or`** 。

未編碼的範例如下所示：

- 字串：`?filter=Field operator 'Value'`
- 布林值：`?filter=Field operator Value`
- 包含`?filter=contains(field,'value')`

### <a name="filter-fields"></a>篩選欄位

要求的 filter 參數包含在回應中篩選資料列的一或多個陳述式。 每個語句都包含與或運算子相關聯的欄位和值 **`eq`** **`ne`** 。 有些欄位也支援 **`contains`** 、 **`gt`** 、、 **`lt`** **`ge`** 和 **`le`** 運算子。 語句可以使用 **`and`** or 運算子來結合 **`or`** 。

以下是篩選字串的範例：

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

下表顯示篩選參數支援的欄位和支援運算子清單。 字串值必須以單引號括住。

| 參數 | 支援的運算子 | Description |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | 值，指出是否自動更新訂用帳戶。 |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | 訂閱結束的日期。 |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | 建立訂用帳戶的日期。 |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | 訂用帳戶的目前狀態將會變更的日期。 |
| customerMarket | `eq`, `ne` | 客戶執行業務的國家/地區。 |
| customerName | `contains` | 客戶的名稱。 |
| customerTenantId | `eq`, `ne` | GUID 格式的字串，可識別客戶租使用者。 |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | 取消布建訂用帳戶的日期。 預設值為 null。 |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | 訂用帳戶開始的日期。 |
| friendlyName | `contains` | 訂閱的名稱。 |
| id | `eq`, `ne` | 用來識別訂用帳戶的 GUID 格式字串。 |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | 上次更新訂用帳戶的日期。 預設值為 null。 |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | 上次使用訂用帳戶的日期。 預設值為 null。 |
| partnerId | `eq`, `ne` | MPN 識別碼。 若為直接轉銷商，此值會是合作夥伴的 MPN 識別碼。 若為間接轉銷商，此值將是間接轉銷商的 MPN 識別碼。 |
| partnerName | 字串 | 購買訂閱之夥伴的名稱 |
| productName | `contains`, `eq`, `ne` | 產品的名稱。 |
| providerName | 字串 | 若為間接轉銷商的訂閱交易，提供者名稱就是購買訂閱的間接提供者。|
| status | `eq`, `ne` | 訂用帳戶狀態。 支援的值為： "ACTIVE"、"暫止" 或 "取消布建"。 |
| subscriptionType | `eq`, `ne` | 訂閱類型。 **注意**：此欄位會區分大小寫。 支援的值為： "Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS"。 |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | 訂用帳戶的試用期開始日期。 預設值為 null。 |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | 訂用帳戶從試用版轉換成付費的日期。 預設值為 null。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含符合篩選準則的[訂](partner-center-analytics-resources.md#subscription-resource)用帳戶資源集合。

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
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a>另請參閱

- [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
