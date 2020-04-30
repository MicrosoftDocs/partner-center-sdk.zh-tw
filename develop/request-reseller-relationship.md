---
title: 擷取關聯性的要求 URL
description: 如何取得要傳送給客戶的關聯性要求 URL。
ms.assetid: 31D9EDB2-4ABE-4C57-A394-2FF256F7D3CA
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: de6eaa1451e91df29f6a9ed0448e70b348b1e64c
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157000"
---
# <a name="retrieve-a-relationship-request-url"></a>擷取關聯性的要求 URL

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何取得要傳送給客戶的關聯性要求 URL。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

## <a name="c"></a>C\#

若要取出關聯性要求 URL，請先使用[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers)來取得合作夥伴客戶作業的介面。 接下來，使用[**RelationshipRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest)屬性來取得客戶關係要求作業的介面。 最後，呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync)方法來取出 URL。

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： GetCustomerRelationshipRequest.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                            |
|---------|----------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

None

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，回應會包含[RelationshipRequest](relationships-resources.md#relationshiprequest)物件。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://portal.office.com/partner/partnersignup.aspx?type=ResellerRelationship&id=3b33e682-00c3-41ee-9dd2-a548adf56438&csp=1&msppid=0",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
