---
title: 為客戶檢視已刪除的使用者
description: 取得客戶的已刪除 CustomerUser 資源清單（依客戶識別碼）。 您可以選擇性地設定頁面大小。 您必須提供篩選準則。
ms.assetid: B2248C7D-0F68-4F52-9249-D3168C2F6E83
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cab6b1cd309757f0754610eca362bcf205d199fb
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414247"
---
# <a name="view-deleted-users-for-a-customer"></a>為客戶檢視已刪除的使用者


**適用於**

- 夥伴中心

取得客戶的已刪除 CustomerUser 資源清單（依客戶識別碼）。 您可以選擇性地設定頁面大小。 您必須提供篩選準則。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼。

## <a name="span-idwhat_happens_when_you_delete_a_user_account_span-idwhat_happens_when_you_delete_a_user_account_span-idwhat_happens_when_you_delete_a_user_account_what-happens-when-you-delete-a-user-account"></a><span id="What_happens_when_you_delete_a_user_account_"/><span id="what_happens_when_you_delete_a_user_account_"/><span id="WHAT_HAPPENS_WHEN_YOU_DELETE_A_USER_ACCOUNT_"/>當您刪除使用者帳戶時，會發生什麼事？


當您刪除使用者帳戶時，使用者狀態會設定為「非作用中」。 在30天內，它會維持這種方式，在此之後，使用者帳戶及其相關聯的資料會被清除並使其無法復原。 如果您想要在三十天的時間範圍內還原已刪除的使用者帳戶，請參閱[為客戶還原已刪除的使用者](restore-a-user-for-a-customer.md)。 請注意，一旦刪除並標示為「非作用中」，使用者帳戶就不會再以使用者集合的成員身分傳回（例如，使用[取得客戶的所有使用者帳戶清單](get-a-list-of-all-user-accounts-for-a-customer.md)）。 若要取得尚未清除的已刪除使用者清單，您必須查詢已設定為非使用中的使用者帳戶。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要抓取已刪除的使用者清單，請建立查詢，以篩選其狀態設定為非作用中的客戶使用者。 首先，使用參數具現化[**SimpleFieldFilter**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter)物件來建立篩選，如下列程式碼片段所示。 然後使用[**BuildIndexedQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery)方法來建立查詢。 請注意，如果您不想要分頁結果，可以改用[**BuildSimpleQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)方法。 接下來，使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法搭配客戶識別碼來識別客戶。 最後，呼叫[**查詢**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query)方法來傳送要求。

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： GetCustomerInactiveUsers.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求


**要求語法**

| 方法  | 要求 URI                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/users？ size = {size} & 篩選準則 = {FILTER} HTTP/1。1 |

 

**URI 參數**

建立要求時，請使用下列路徑和查詢參數。

| 名稱        | 類型   | 必要項 | 描述                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 客戶識別碼 | guid   | 是      | 此值是可識別客戶的 GUID 格式客戶識別碼。                                                                                                            |
| size        | int    | 否       | 要一次顯示的結果數目。 這個參數是選擇性的。                                                                                                     |
| 篩選器      | 篩選器 | 是      | 篩選使用者搜尋的查詢。 若要取出已刪除的使用者，您必須包含下列字串並為其編碼： {"Field"： "UserState"，"Value"： "非使用中"，"Operator"： "equals"}。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 回應


如果成功，此方法會在回應主體中傳回[CustomerUser](user-resources.md#customeruser)資源的集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




