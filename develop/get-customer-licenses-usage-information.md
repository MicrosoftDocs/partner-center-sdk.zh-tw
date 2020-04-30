---
title: 取得客戶授權使用資訊
description: 如何取得特定客戶的授權使用量見解。
ms.assetid: 02B98495-9FE7-4A9F-B1DD-B14563D0FF29
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7d853665bf4f7e9cac8e58871416d3f67c86cfe5
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157540"
---
# <a name="get-customer-licenses-usage-information"></a>取得客戶授權使用資訊

**適用于**

- 合作夥伴中心

如何取得特定客戶的授權部署深入解析。

> [!NOTE]
> 此案例是透過[取得授權使用資訊](get-licenses-usage-information.md)來取代。

## <a name="prerequisites"></a>Prerequisites

認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。

## <a name="c"></a>C\#

若要針對指定的客戶抓取部署上的匯總資料，請先呼叫[**iaggregatepartner.customers.byid 的 ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，並提供客戶識別碼來識別客戶。 然後從 [[**分析**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics)] 屬性取得客戶層級分析集合作業的介面。 接下來，從 [[**授權**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses)] 屬性取得客戶層級授權分析集合的介面。 最後，請呼叫[**usage**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get)方法來取得授權使用量的匯總資料。 如果方法成功，您會取得[**CustomerLicensesUsageInsights**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights)物件的集合。

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列路徑參數來識別客戶。

| 名稱        | 類型 | 必要 | 描述                                                |
|-------------|------|----------|------------------------------------------------------------|
| customer-id | guid | 是      | 識別客戶的 GUID 格式客戶識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應本文會包含[CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights)資源的集合，以提供授權使用方式的相關資訊。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1726
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CV: 0mufM0K1kEOoR7oI.0
MS-ServerId: 030020525
Date: Wed, 15 Mar 2017 01:19:58 GMT

{
    "totalCount": 5,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesActive": 0,
            "licensesQualified": 5,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesActive": 0,
            "licensesQualified": 2,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
