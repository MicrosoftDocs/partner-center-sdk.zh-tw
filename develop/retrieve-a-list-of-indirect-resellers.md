---
title: 擷取間接轉銷商清單
description: 如何取出已登入合作夥伴的間接轉銷商清單。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d7b8962c24a00ac6892279e7b7c08c4144514f3
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "91007706"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>擷取間接轉銷商清單

**適用於**

- 合作夥伴中心

如何取出已登入合作夥伴的間接轉銷商清單。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

## <a name="c"></a>C\#

若要抓取已登入夥伴具有關聯性的間接轉銷商清單，請先從 [**PartnerOperations 關聯**性/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) 屬性取得關聯性集合作業的介面。 然後，呼叫 [**get**/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) 或 [**get \_ Async**/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) 方法，傳遞 [**PartnerRelationshipType**/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) 列舉的成員來識別關聯性類型。 若要擷取間接轉銷商，您必須使用 IsIndirectCloudSolutionProviderOf。

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**範例**： [主控台測試應用程式](console-test-app.md)**專案**：合作夥伴中心 SDK 範例 **類別**： GetIndirectResellers.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/relationships？關聯性 \_ 類型 = >isindirectcloudsolutionproviderof HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來識別關聯性類型。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>類型</th>
<th>必要</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>relationship_type</td>
<td>字串</td>
<td>Yes</td>
<td>值是在 <a href="/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype"><strong>PartnerRelationshipType</strong></a>中找到的其中一個成員名稱的字串表示。
<p>如果夥伴以提供者的身份登入，而您想要取得他們已建立關聯性的間接轉銷商清單，請使用 >isindirectcloudsolutionproviderof。</p>
<p>如果夥伴以轉銷商的身份登入，而您想要取得他們已建立關聯性的間接提供者清單，請使用 IsIndirectResellerOf。</p></td>
</tr>
</tbody>
</table>

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應本文會包含用來識別轉售商的 [PartnerRelationship](relationships-resources.md) 資源集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
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