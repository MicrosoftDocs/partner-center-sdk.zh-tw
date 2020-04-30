---
title: 更新服務要求
description: 如何更新雲端解決方案提供者已代表客戶向 Microsoft 提出的現有客戶服務要求。
ms.assetid: 09C13775-739B-4CB9-9442-456E17F91452
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ca618afa6e5dc2b6db141ec8a590554b9592eb94
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157940"
---
# <a name="update-a-service-request"></a>更新服務要求

**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何更新雲端解決方案提供者已代表客戶向 Microsoft 提出的現有客戶服務要求。

在合作夥伴中心儀表板中，您可以先[選取客戶](get-a-customer-by-name.md)來執行這項作業。 然後，選取左側提要欄位上的 [**服務管理**]。 在 [**支援要求**] 標頭底下，選取有問題的服務要求。 若要完成，請對服務要求進行所需的變更，然後選取 [**提交]。**

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 服務要求識別碼。

## <a name="c"></a>C\#

若要更新客戶的服務要求，請使用服務要求識別碼呼叫[**IServiceRequestCollection. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid)方法，以識別並傳回服務要求介面。 然後，呼叫[**IServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch)或[**PatchAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync)方法來更新服務要求。 若要提供更新的值，請建立新的空白[**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)物件，並只設定您想要變更的屬性值。 然後在對 Patch 或 PatchAsync 方法的呼叫中傳遞該物件。

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： UpdatePartnerServiceRequest.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **跳** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列 URI 參數來更新服務要求。

| 名稱                  | 類型     | 必要 | 描述                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **servicerequest-id** | **guid** | Y        | 識別服務要求的 GUID。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求主體應包含[ServiceRequest](service-request-resources.md)資源。 唯一必要的值是要更新的值。

### <a name="request-example"></a>要求範例

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回**服務要求**資源，並在回應主體中包含更新的屬性。

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
