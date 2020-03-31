---
title: 建立服務要求
description: 如何建立合作夥伴中心服務要求。
ms.assetid: 16DA9836-7052-4103-82D4-933E5EEB7E71
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e2060beb7b276e76c29e7bc92e0543aa41a703b1
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413847"
---
# <a name="create-a-service-request"></a>建立服務要求

適用於：

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何建立合作夥伴中心服務要求。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 支援主題識別碼。 如果您沒有支援主題識別碼，請參閱[取得服務要求支援主題](get-service-request-support-topics--pending-.md)。

## <a name="c"></a>C\#

若要建立服務要求：

1. 建立並填入具有標題、描述、嚴重性和支援主題識別碼的[**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)物件。為了新增其他資訊， [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)物件支援選擇性的[**附注**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.notes)集合，但不支援檔案的連結以進行上傳。
2. 建立物件之後，請呼叫[**iaggregatepartner.customers.byid. ServiceRequests. Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.ipartnerservicerequestcollection.create)方法，將新建立的 ServiceRequest 物件和包含建立服務要求之組織地區設定的字串（代理程式地區設定）傳遞給它。

### <a name="c-example"></a>C\# 範例

``` csharp
// IAggregatePartner partnerOperations;
// string supportTopicId;

ServiceRequest serviceRequestToCreate = new ServiceRequest()
{
    Title = "TrialSR",
    Description = "Ignore this SR",
    Severity = ServiceRequestSeverity.Critical,
    SupportTopicId = supportTopicId
};

ServiceRequest serviceRequest = partnerOperations.ServiceRequests.Create(serviceRequestToCreate, "en-US");
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： CreatePartnerServiceRequest.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/servicerequests/{agent-locale} HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

使用下列 URI 參數來識別代理程式的地區設定。

| 名稱             | 類型       | 必要項 | 描述                                                  |
|------------------|------------|----------|--------------------------------------------------------------|
| **代理程式-地區設定** | **字串** | Y        | 建立服務要求的組織地區設定。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的必要和選擇性屬性。

| 名稱             | 類型                                                                        | 必要項 | 描述                                                                          |
|------------------|-----------------------------------------------------------------------------|----------|--------------------------------------------------------------------------------------|
| 標題            | string                                                                      | Y        | 服務要求標題。                                                           |
| 描述      | string                                                                      | Y        | 描述。                                                                     |
| Severity         | string                                                                      | Y        | 嚴重性：「不明」、「重大」、「適中」或「最小」。                       |
| SupportTopicId   | string                                                                      | Y        | 支援主題的識別碼。                                                         |
| SupportTopicName | string                                                                      | N        | 支援主題的名稱。                                                       |
| Id               | string                                                                      | N        | 服務要求的識別碼。                                                       |
| 狀態           | string                                                                      | N        | 服務要求的狀態： [無]、[開啟]、[已關閉] 或 [\_需要注意]。 |
| 組織     | [ServiceRequestOrganization](service-request-resources.md#servicerequestorganization) | N        | 建立服務要求的組織。                               |
| primaryContact   | [ServiceRequestContact](service-request-resources.md#servicerequestcontact)           | N        | 服務要求的主要連絡人。                                              |
| LastUpdatedBy    | [ServiceRequestContact](service-request-resources.md#servicerequestcontact)           | N        | 「上次更新者」連絡人，以瞭解服務要求的變更。                        |
| ProductName      | string                                                                      | N        | 對應至服務要求的產品名稱。                     |
| ProductId        | string                                                                      | N        | 產品的識別碼。                                                               |
| CreatedDate      | date                                                                        | N        | 服務要求建立的日期。                                          |
| lastModifiedDate | date                                                                        | N        | 上次修改服務要求的日期。                                 |
| LastClosedDate   | date                                                                        | N        | 上次關閉服務要求的日期。                                   |
| FileLinks        | [FileInfo](utility-resources.md#fileinfo)資源的陣列               | N        | 與服務要求相關之檔案連結的集合。                    |
| NewNote          | [ServiceRequestNote](service-request-resources.md#servicerequestnote)                 | N        | 附注可以加入至現有的服務要求。                                  |
| 注意事項            | [ServiceRequestNotes](service-request-resources.md#servicerequestnote)的陣列       | N        | 加入至服務要求的附注集合。                                  |
| CountryCode      | string                                                                      | N        | 對應至服務要求的國家/地區。                                    |
| 屬性       | object                                                                      | N        | 包含 "ObjectType"： "ServiceRequest"。                                             |

下表描述要求主體中的必要屬性。

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/servicerequests/en-US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 474
Expect: 100-continue

{
    "Id": null,
    "Title": "TrialSR",
    "Description": "Ignore this SR",
    "Severity": "critical",
    "SupportTopicId": "32444671",
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
    "NewNote": null,
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**服務要求**資源屬性。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 201 Created
Content-Length: 721
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CV: vB9EuWs/ukaxQmuV.0
MS-ServerId: 101112616
Date: Thu, 22 Dec 2016 20:31:14 GMT

 {
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "id": "616122292874576",
    "status": "none",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1",
        "phoneNumber": "2398391056"
    },
    "primaryContact": {
        "organization": {
            "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "name": "TEST_TEST_BugBash1",
            "phoneNumber": "2398391056"
        },
        "contactId": "bb4ebcf5-d84c-4b35-8469-f4cfa4ac909e",
        "lastName": "Account",
        "email": "admin@testtestbugbash1.onmicrosoft.com",
        "phoneNumber": "2066017143"
    },
    "createdDate": "0001-01-01T00:00:00",
    "lastModifiedDate": "0001-01-01T00:00:00",
    "lastClosedDate": "0001-01-01T00:00:00",
    "countryCode": "US",
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```