---
title: 取得合作夥伴授權使用資訊
description: 如何取得匯總的合作夥伴授權使用量資訊，以包含所有客戶。
ms.assetid: 87BCC8FC-5C29-4245-8607-BB62ABC03EDE
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f33af84c8a0e7fcf7b5720d0dd2aa1219bc65781
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157330"
---
# <a name="get-partner-licenses-usage-information"></a>取得合作夥伴授權使用資訊

**適用于**

- 合作夥伴中心

如何取得匯總的合作夥伴授權使用量資訊，以包含所有客戶。

> [!NOTE]
> 此案例是透過[取得授權使用資訊](get-licenses-usage-information.md)來取代。

## <a name="prerequisites"></a>Prerequisites

認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。

## <a name="c"></a>C\#

若要在授權部署上取得匯總資料，請先從[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.analytics)屬性取得合作夥伴層級分析集合作業的介面。 然後從 [[**授權**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses)] 屬性，將介面抓取到夥伴層級授權分析集合。 最後，請呼叫[**usage**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get)方法來取得授權使用量的匯總資料。 如果方法成功，您會取得[**PartnerLicensesUsageInsights**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights)物件的集合。

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                      |
|---------|----------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights)資源的集合，以提供所使用之授權的相關資訊。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1156
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CV: wk0/vjugzEe0Z9cv.0
MS-ServerId: 101112012
Date: Wed, 15 Mar 2017 01:18:26 GMT

{
    "totalCount": 5,
    "items": [{
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Microsoft Dynamics CRM",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
