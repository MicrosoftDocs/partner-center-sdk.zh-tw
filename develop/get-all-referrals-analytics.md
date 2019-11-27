---
title: 取得所有推薦的分析資訊
description: 如何取得所有的參考分析資訊。
ms.assetid: C6051714-1D8A-4448-9705-12AEC9A6420E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d5ad0ad0eedcce633940daa6356e2a2e1e9220c5
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485948"
---
# <a name="get-all-referrals-analytics-information"></a>取得所有推薦的分析資訊

**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


如何為您的客戶取得所有的參考分析資訊。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例僅支援使用使用者認證進行驗證。 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求語法**

| 方法  | 要求 URI |
|---------|-------------|
| **獲取** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1。1 |
 

**URI 參數**

| 參數 | 類型 | 描述 |
|-----------|------|-------------|
| filter | 字串 | 傳回符合篩選準則的資料。</br> **範例：**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | 字串 |    支援條款和日期。 用來限制值區數目的短路邏輯。</br> **範例：**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | 字串 |   *AggregationLevel*參數需要*groupby*。 *AggregationLevel*參數會套用到出現在*groupby*中的所有日期欄位。</br> **範例：**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | 字串 | 頁面限制為10000。 採用小於10000的任何值。</br> **範例：**</br> `.../referrals?top=100`</br> |
| skip | 字串 |   要略過的資料列數目。</br> **範例：**</br>  `.../referrals?top=100&skip=100` |

  
**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

無。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應主體會包含[參考](partner-center-analytics-resources.md#referrals)資源的集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>另請參閱
 - [合作夥伴中心分析-資源](partner-center-analytics-resources.md)
