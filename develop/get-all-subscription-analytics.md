---
title: 取得所有訂用帳戶的分析資訊
description: 如何取得所有訂用帳戶分析資訊。
ms.assetid: 243E54BD-EA34-400E-B9AB-D735EB46B9F6
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b0afac55646980fb59f9cc42051a5532f45bf223
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156440"
---
# <a name="get-all-subscription-analytics-information"></a>取得所有訂用帳戶的分析資訊

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本文說明如何取得客戶的所有訂用帳戶分析資訊。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI |
|--------|-------------|
| **GET** | baseURL/partner/v1/analytics/subscriptions HTTP/1.1 [* \{ \} *](partner-center-rest-urls.md) |

#### <a name="uri-parameters"></a>URI 參數

下表列出選擇性參數和其描述：

| 參數 | 類型 |  描述 |
|-----------|------|--------------|
| top | int | 在要求中傳回的資料列數目。 如果未指定值，則最大值和預設值為`10000`。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。 |
| skip | int | 在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 例如， `top=10000`和`skip=0`會抓取前10000個數據列， `top=10000`並`skip=10000`抓取接下來的10000個數據列。 |
| filter | 字串 | 一或多個篩選回應中資料列的陳述式。 每個篩選語句都會包含回應主體的功能變數名稱，以及與**`eq`**、 **`ne`** 或相關聯的值，適用于特定欄位的**`contains`** 運算子。 語句可以使用**`and`** 或**`or`** 結合。 **篩選** 參數中的字串值必須由單引號括住。 請參閱下一節，以取得可篩選的欄位清單，以及這些欄位支援的運算子。 |
| aggregationLevel | 字串 | 指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：**day**、**week** 或 **month**。 如果未指定值，則預設為**dateRange**。 只有在將日期欄位當做**groupBy**參數的一部分傳遞時，此參數才適用。 |
| groupBy | 字串 | 將資料彙總僅套用至指定欄位的陳述式。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[**訂**](partner-center-analytics-resources.md#subscription-resource)用帳戶資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a>另請參閱

- [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
