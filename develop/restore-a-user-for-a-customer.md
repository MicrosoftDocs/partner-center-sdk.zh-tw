---
title: 為客戶還原已刪除的使用者
description: 如何依客戶識別碼和使用者識別碼還原已刪除的使用者。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d46983b487817fc7152420af1b9332b53dba77b
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926472"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>為客戶還原已刪除的使用者

**適用於**

- 合作夥伴中心

如何依客戶識別碼和使用者識別碼還原已刪除的 **使用者** 。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 使用者識別碼。 如果您沒有使用者識別碼，請參閱 [為客戶查看已刪除的使用者](view-a-deleted-user.md)。

## <a name="when-can-you-restore-a-deleted-user-account"></a>何時可以還原已刪除的使用者帳戶？

當您刪除使用者帳戶時，使用者狀態會設定為「非作用中」。 這種方式會在30天內保持不變，之後使用者帳戶及其相關聯的資料就會被清除並成為無法復原。 您只能在這個三十天的時間範圍內還原已刪除的使用者帳戶。 一旦刪除並標示為「非使用中」，使用者帳戶就不會再以使用者集合的成員形式傳回 (例如，使用 [取得客戶) 的所有使用者帳戶清單](get-a-list-of-all-user-accounts-for-a-customer.md) 。

## <a name="c"></a>C\#

若要還原使用者，請建立 [**>customeruser**/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) 類別的新實例，並將 **[/dotnet/api/microsoft.store.partnercenter.models.users.user.state]**) 屬性的值設定為 [**UserState. 主動**/dotnet/api/microsoft.store.partnercenter.models.users.userstate) 。

您可以藉由將使用者的狀態設定為 [作用中]，來還原已刪除的使用者。 您不必重新擴展使用者資源中的其餘欄位。 這些值會自動從已刪除、非使用中的使用者資源還原。 接下來，使用 [**>iaggregatepartner.customers**] 的 [>iaggregatepartner.customers.byid/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法與客戶識別碼來識別客戶，並使用 [**>iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) 方法來識別使用者。

最後，呼叫 [**Patch**/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) 方法，並傳遞 **>customeruser** 實例以傳送還原使用者的要求。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： CustomerUserRestore.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **補丁** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來指定客戶識別碼和使用者識別碼。

| 名稱                   | 類型     | 必要 | 描述                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 此值是 GUID 格式的 **客戶租使用者識別碼** ，可讓轉銷商將結果篩選至指定的客戶。 |
| **使用者識別碼**            | **guid** | Y        | 此值是屬於單一使用者帳戶的 GUID 格式 **使用者識別碼** 。                                         |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的必要屬性。

| 名稱       | 類型   | 必要 | 描述                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| State      | 字串 | Y        | 使用者狀態。 若要還原已刪除的使用者，此字串必須包含 "active"。 |
| 屬性 | 物件 (object) | N        | 包含 "ObjectType"： ">customeruser"。                                 |

### <a name="request-example"></a>要求範例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，回應會傳迴響應主體中已還原的使用者資訊。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
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
```
