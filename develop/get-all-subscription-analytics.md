---
title: Get all subscription analytics information
description: How to get all the subscription analytics information.
ms.assetid: 243E54BD-EA34-400E-B9AB-D735EB46B9F6
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a6b3d77dc23a0246d168979f754a3c1be5a2a02d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485848"
---
# <a name="get-all-subscription-analytics-information"></a>Get all subscription analytics information

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

This topic describes how to get all the subscription analytics information for your customers.

## <a name="prerequisites"></a>必要條件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI |
|--------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>URI 參數

The following table lists optional parameters and their descriptions:

| 參數 | 在工作列搜尋方塊中輸入 |  說明 |
|-----------|------|--------------|
| top | 整數 | 在要求中傳回的資料列數目。 If the value is not specified, the maximum value and the default value are `10000`. 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。 |
| skip | 整數 | 在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data. |
| filter | 字串 | 一或多個篩選回應中資料列的陳述式。 Each filter statement contains a field name from the response body and a value that are associated with the **eq**, **ne**, or for certain fields, the **contains** operator. 陳述式可以使用 **and** 或 **or** 來結合。 **篩選** 參數中的字串值必須由單引號括住。 See the following section for a list of fields that can be filtered and the operators that are supported with those fields. |
| aggregationLevel | 字串 | 指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：**day**、**week** 或 **month**。 If the value is not specified, the default is **dateRange**. This parameter applies only when a date field is passed as part of the **groupBy** parameter. |
| groupBy | 字串 | 將資料彙總僅套用至指定欄位的陳述式。 |

### <a name="request-headers"></a>要求標頭

See [Headers](headers.md) for more information.

### <a name="request-body"></a>要求主體

無。

### <a name="request-example"></a>要求的範例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST response

If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription) resources.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

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

## <a name="see-also"></a>請參閱

- [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
