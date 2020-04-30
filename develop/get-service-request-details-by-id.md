---
title: 依識別碼取得服務要求詳細資料。
description: 如何依識別碼取得現有客戶服務要求的詳細資料。
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a99a470eb7abd0d16cfa4e73abe0e720542e274a
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157260"
---
# <a name="get-service-request-details-by-id"></a>依照識別碼取得服務要求詳細資料

**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何使用服務要求識別碼來取得現有客戶服務要求的詳細資料。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 服務要求識別碼。

## <a name="c"></a>C\#

若要取得現有客戶服務要求的詳細資料，請呼叫[**IServiceRequestCollection. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid)方法，並傳入[**ServiceRequest.Id**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id)來識別並將介面傳回給特定的[**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)物件。

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest as ServiceRequest;

ServiceRequest serviceRequestDetails = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Get();

Console.WriteLine(string.Format("The primary contact for the service request {0} is {1} {2}.",
    serviceRequestDetails.Title,
    serviceRequestDetails.PrimaryContact.FirstName,
    serviceRequestDetails.PrimaryContact.LastName,
));
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1。1  |

### <a name="uri-parameter"></a>URI 參數

使用下列 URI 參數來取得指定的服務要求。

| 名稱                  | 類型     | 必要 | 描述                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **servicerequest-id** | **guid** | Y        | 識別服務要求的 GUID。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**服務要求**資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
