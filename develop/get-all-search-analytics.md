---
title: 取得所有搜尋的分析資訊
description: 如何取得所有搜尋分析資訊。
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093972"
---
# <a name="get-all-search-analytics-information"></a>取得所有搜尋的分析資訊

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何取得客戶的所有搜尋分析資訊。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI |
|---------|-------------|
| **GET** | [* \{ BASEURL \} *](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

|    參數     |  類型  |                                                                                                                   Description                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter      | 字串 |                                                                     傳回符合篩選準則的資料。 </br> **範例︰**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | 字串 |                                         支援條款和日期。 用來限制值區數目的短路邏輯。 </br> **範例︰**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | 字串 | *AggregationLevel*參數需要*groupby*。 *AggregationLevel*參數會套用到出現在*groupby*中的所有日期欄位。 </br> **範例︰**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | 字串 |                                                                     頁面限制為10000。 採用小於10000的任何值。  </br> **範例︰**</br>  `.../search?top=100`                                                                     |
|       skip       | 字串 |                                                                                  要略過的資料列數目。 </br> **範例︰**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[搜尋](partner-center-analytics-resources.md#search-resource)資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a>另請參閱

- [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
