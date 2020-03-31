---
title: 取得間接轉銷商清單
description: 如何抓取已登入之合作夥伴的間接轉銷商清單。
ms.assetid: 1767BD6C-651A-4C14-930B-35D7EFD46C19
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a1ed1d4d3c0d105a489774d698d832f2e0212934
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415376"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>取得間接轉銷商清單


**適用於**

- 夥伴中心

如何抓取已登入之合作夥伴的間接轉銷商清單。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取出已登入夥伴具有關聯性的間接轉銷商清單，請先從[**partnerOperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.relationships)屬性取得關聯性集合作業的介面。 然後，呼叫[**get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get)或[**get\_Async**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync)方法，傳遞[**PartnerRelationshipType**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)列舉的成員來識別關聯性類型。 若要取出間接轉銷商，您必須使用 IsIndirectCloudSolutionProviderOf。

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**範例**：[主控台測試應用程式](console-test-app.md)**專案**：合作夥伴中心 SDK 範例**類別**： GetIndirectResellers.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法  | 要求 URI                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/relationships？關聯性\_類型 = IsIndirectCloudSolutionProviderOf HTTP/1。1 |

 

**URI 參數**

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
<th>必要項</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>relationship_type</td>
<td>string</td>
<td>是</td>
<td>值是在<a href="https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype"><strong>PartnerRelationshipType</strong></a>中找到的其中一個成員名稱的字串表示。
<p>如果合作夥伴以提供者身分登入，而您想要取得他們已建立關聯性的間接轉銷商清單，請使用 IsIndirectCloudSolutionProviderOf。</p>
<p>如果合作夥伴以轉銷商的身分登入，而您想要取得他們已建立關聯性的間接提供者清單，請使用 IsIndirectResellerOf。</p></td>
</tr>
</tbody>
</table>

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
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

 

 




