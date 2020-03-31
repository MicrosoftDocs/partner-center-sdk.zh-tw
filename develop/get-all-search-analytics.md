---
title: 取得所有搜尋分析資訊
description: 如何取得所有搜尋分析資訊。
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: fc686891cf80e67eab01540a77b3335f23bdc598
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416085"
---
# <a name="get-all-search-analytics-information"></a>取得所有搜尋分析資訊

**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


如何取得客戶的所有搜尋分析資訊。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求語法**

| 方法  | 要求 URI |
|---------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1。1 |

 

**URI 參數**


|    參數     |  類型  |                                                                                                                   描述                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      篩選器      | string |                                                                     傳回符合篩選準則的資料。 </br> **範例：**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | string |                                         支援條款和日期。 用來限制值區數目的短路邏輯。 </br> **範例：**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | string | *AggregationLevel*參數需要*groupby*。 *AggregationLevel*參數會套用到出現在*groupby*中的所有日期欄位。 </br> **範例：**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       上        | string |                                                                     頁面限制為10000。 採用小於10000的任何值。  </br> **範例：**</br>  `.../search?top=100`                                                                     |
|       skip       | string |                                                                                  要略過的資料列數目。 </br> **範例：**</br> `.../search?top=100&skip=100`                                                                                   |
  
**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應主體會包含[搜尋](partner-center-analytics-resources.md#search_resource)資源的集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>另請參閱
 - [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
