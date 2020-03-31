---
title: 取得客戶的間接轉售商
description: 如何取得與指定客戶有關聯性的間接轉銷商清單。
ms.assetid: C3C4BE9A-97E8-41AD-AB28-6F9CB7DCE475
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: aa6ac902435c1e125e379c1b016f6aef7347b54d
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415931"
---
# <a name="get-indirect-resellers-of-a-customer"></a>取得客戶的間接轉售商

**適用於**

- 夥伴中心

如何取得與指定客戶有關聯性的間接轉銷商清單。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要抓取指定的客戶具有關聯性的間接轉售商清單，請先提供客戶識別碼來識別客戶，以從[**partnerOperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.relationships)中取得特定客戶的客戶集合作業介面。 然後呼叫[**關聯性。 get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get)或[**get\_Async**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync)方法，以取得間接轉銷商的清單。

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)**專案**：合作夥伴中心 SDK 範例**類別**： GetIndirectResellersOfCustomer.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1。1 |

 

**URI 參數**

使用下列 path 參數來識別客戶。

| 名稱        | 類型   | 必要項 | 描述                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 客戶識別碼 | string | 是      | 識別客戶的 GUID 格式字串。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應

如果成功，回應主體會包含[PartnerRelationship](relationships-resources.md)資源的集合，以識別轉售商。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```