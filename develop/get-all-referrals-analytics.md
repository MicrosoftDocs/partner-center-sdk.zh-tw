---
title: 取得所有轉介的分析資訊
description: 如何取得所有的參考分析資訊。
ms.assetid: C6051714-1D8A-4448-9705-12AEC9A6420E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 397e36cf45fd2a43af58585ab8162a01086316b9
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156580"
---
# <a name="get-all-referrals-analytics-information"></a>取得所有轉介的分析資訊

**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何為您的客戶取得所有的參考分析資訊。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI |
|---------|-------------|
| **GET** | baseURL/partner/v1/analytics/referrals HTTP/1.1 [* \{ \} *](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>URI 參數

| 參數 | 類型 | 描述 |
|-----------|------|-------------|
| filter | 字串 | 傳回符合篩選準則的資料。</br> **範例：**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | 字串 | 支援條款和日期。 用來限制值區數目的短路邏輯。</br> **範例：**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | 字串 | *AggregationLevel*參數需要*groupby*。 *AggregationLevel*參數會套用到出現在*groupby*中的所有日期欄位。</br> **範例：**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | 字串 | 頁面限制為10000。 採用小於10000的任何值。</br> **範例：**</br> `.../referrals?top=100`</br> |
| skip | 字串 | 要略過的資料列數目。</br> **範例：**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[參考](partner-center-analytics-resources.md#referrals-resource)資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a>另請參閱

- [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
