---
title: 為客戶檢視已刪除的使用者
description: 取得客戶的已刪除 >customeruser 資源清單（依客戶識別碼）。 您可以選擇性地設定頁面大小。 您必須提供篩選準則。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dd7b573cca5810195d840fcb729850f981e55a51
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925542"
---
# <a name="view-deleted-users-for-a-customer"></a>為客戶檢視已刪除的使用者

**適用於**

- 合作夥伴中心

取得客戶的已刪除 >customeruser 資源清單（依客戶識別碼）。 您可以選擇性地設定頁面大小。 您必須提供篩選準則。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

## <a name="what-happens-when-you-delete-a-user-account"></a>當您刪除使用者帳戶時，會發生什麼事？

當您刪除使用者帳戶時，使用者狀態會設定為「非作用中」。 這種方式會在30天內保持不變，之後使用者帳戶及其相關聯的資料就會被清除並成為無法復原。 如果您想要在三十天內還原已刪除的使用者帳戶，請參閱 [為客戶還原已刪除的使用者](restore-a-user-for-a-customer.md)。 一旦刪除並標示為「非使用中」，使用者帳戶就不會再以使用者集合的成員形式傳回 (例如，使用 [取得客戶) 的所有使用者帳戶清單](get-a-list-of-all-user-accounts-for-a-customer.md) 。 若要取得尚未清除的已刪除使用者清單，您必須查詢已設定為非使用中的使用者帳戶。

## <a name="c"></a>C\#

若要抓取已刪除的使用者清單，請建立一個查詢，以篩選其狀態設為非作用中的客戶使用者。 首先，使用下列程式碼片段中所示的參數具現化 [**>simplefieldfilter**/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) 物件，以建立篩選。 然後使用 [**BuildIndexedQuery**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) 方法來建立查詢。 如果您不想要分頁結果，可以改用 [**>buildsimplequery**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) 方法。 接下來，使用 [**>iaggregatepartner.customers. >iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法與客戶識別碼來識別客戶。 最後，呼叫 [**Query**/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) 方法來傳送要求。

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

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users？ size = {size} &filter = {FILTER} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

建立要求時，請使用下列路徑和查詢參數。

| 名稱        | 類型   | 必要 | 描述                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| customer-id | guid   | Yes      | 此值是可識別客戶的 GUID 格式化客戶識別碼。                                                                                                            |
| 大小        | int    | 否       | 要一次顯示的結果數目。 這是選擇性參數。                                                                                                     |
| filter      | filter | Yes      | 可篩選使用者搜尋的查詢。 若要擷取已刪除的使用者，您必須包含下列字串並加以編碼：{"Field":"UserState","Value":"Inactive","Operator":"equals"}。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳迴響應主體中 [>customeruser](user-resources.md#customeruser) 資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

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
