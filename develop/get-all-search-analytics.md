---
title: Get all search analytics information
description: How to get all the search analytics information.
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8237786aceaa19a84abf4277b72ba94debf48e6d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485868"
---
# <a name="get-all-search-analytics-information"></a>Get all search analytics information

**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


How to get all the search analytics information for your customers. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only. 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request


**Request syntax**

| 方法  | 要求 URI |
|---------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1 |

 

**URI parameters**


|    參數     |  在工作列搜尋方塊中輸入  |                                                                                                                   說明                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter      | 字串 |                                                                     Returns data matching the filter condition. </br> **範例：**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | 字串 |                                         Supports both terms and dates. Short circuit logic to limit the number of buckets. </br> **範例：**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | 字串 | The *aggregationLevel* parameter requires a *groupby*. The *aggregationLevel* parameter applies to all date fields present in the *groupby*. </br> **範例：**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | 字串 |                                                                     The page limit is 10000. Takes any value less than 10000.  </br> **範例：**</br>  `.../search?top=100`                                                                     |
|       skip       | 字串 |                                                                                  Number of rows to skip. </br> **範例：**</br> `.../search?top=100&skip=100`                                                                                   |
  
**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

無。

**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search_resource) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>See also
 - [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
