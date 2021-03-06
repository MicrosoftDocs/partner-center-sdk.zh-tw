---
title: 驗證網域可用性
description: 如何判斷網域是否可供使用。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3f2e3d551da30c7b9c25e1fc3f3280a425aff8f8
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925584"
---
# <a name="verify-domain-availability"></a>驗證網域可用性

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何判斷網域是否可供使用。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 網域 (例如 `contoso.onmicrosoft.com`) 。

## <a name="c"></a>C\#

若要確認網域是否可用，請先呼叫 [**>iaggregatepartner.customers**/dotnet/api/microsoft.store.partnercenter.ipartner.domains) ，以取得網域作業的介面。 然後，呼叫 [**ByDomain**/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) 方法與要檢查的網域。 這個方法會針對特定網域的可用作業取得介面。 最後，呼叫 [**Exists**/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) 方法，以查看網域是否已存在。

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： CheckDomainAvailability.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                              |
|----------|--------------------------------------------------------------------------|
| **頭** | [*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來確認網域的可用性。

| 名稱       | 類型       | 必要 | 描述                                   |
|------------|------------|----------|-----------------------------------------------|
| **域** | **string** | Y        | 用來識別受檢網域的字串。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無

### <a name="request-example"></a>要求範例

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果網域存在，則無法使用它，而且會傳迴響應狀態碼 200 OK。 如果找不到網域，則可供使用，而且會傳迴響應狀態碼404。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>當網域已在使用中時的回應範例

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>可用網域的回應範例

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
