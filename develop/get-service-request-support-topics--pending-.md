---
title: 取得服務要求支援主題的清單
description: 取得專案的集合，代表服務要求的有效主題。
ms.assetid: 50A61342-70C4-49F5-BEA2-2754338CF5A1
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cccaa14c450e9c73b65172c85e5a09058c9fdef2
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157250"
---
# <a name="get-service-request-support-topics"></a>取得服務要求支援主題的清單

**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得專案的集合，代表服務要求的有效主題。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

## <a name="c"></a>C\#

若要取得服務要求主題的集合，請使用您的[**ipartneroperations.profiles**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner)集合來取出產生之物件的[**ServiceRequests**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.servicerequests)屬性，後面接著[**SupportTopics**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection)屬性和[**get （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection.get)或[**GetAsync （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection.getasync)方法。

``` csharp
// IPartner partnerOperations;

ResourceCollection<SupportTopic> supportTopicsCollection = partnerOperations.ServiceRequests.SupportTopics.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                           |
|---------|---------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/supporttopics HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/supporttopics HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4c1e8b6c-d136-4931-9df9-d85ec08ccffe
MS-CorrelationId: f447b215-f9bc-48da-a05a-3b5322d86a9c
X-Locale: en-US
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回支援要求的有效主題集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 4982
Content-Type: application/json
MS-CorrelationId: f447b215-f9bc-48da-a05a-3b5322d86a9c
MS-RequestId: 4c1e8b6c-d136-4931-9df9-d85ec08ccffe
Date: Fri, 29 Jan 2016 22:31:36 GMT

{
    "totalCount":14,
    "items":[{
        "name":"Partner Center Issues",
        "description":"Office 365 questions from the CSP (Cloud Solution Provider) partners using Partner Center",
        "id":32444667,
        "attributes":{
            "objectType":"SupportTopic"
        }
    },
    {
        "name":"Cannot manage my profile",
        "description":"Issues that are related to errors or problems with managing a profile",
        "id":32444671,
        "attributes":{
            "objectType":"SupportTopic"
        }
    }],
    "attributes":{
        "objectType":"Collection"
    }
}
```
