---
title: 為客戶還原已刪除的使用者
description: 如何依客戶識別碼和使用者識別碼還原已刪除的使用者。
ms.assetid: A48A4718-6EAF-4FC8-8B44-F3FDCA2B3298
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cfedefd5b9b8547b79b817c06f44e9b21f12d51c
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415388"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>為客戶還原已刪除的使用者


**適用於**

- 夥伴中心

如何依客戶識別碼和使用者識別碼還原已刪除的**使用者**。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- 使用者識別碼。 如果您沒有使用者識別碼，請參閱[View deleted users for a customer](view-a-deleted-user.md)。

## <a name="span-idwhen_can_you_restore_a_deleted_user_account_span-idwhen_can_you_restore_a_deleted_user_account_span-idwhen_can_you_restore_a_deleted_user_account_when-can-you-restore-a-deleted-user-account"></a>當您可以還原已刪除的使用者帳戶時，<span id="When_can_you_restore_a_deleted_user_account_"/><span id="when_can_you_restore_a_deleted_user_account_"/><span id="WHEN_CAN_YOU_RESTORE_A_DELETED_USER_ACCOUNT_"/>？


當您刪除使用者帳戶時，使用者狀態會設定為「非作用中」。 在30天內，它會維持這種方式，在此之後，使用者帳戶及其相關聯的資料會被清除並使其無法復原。 您只能在這三十天的時間範圍內還原已刪除的使用者帳戶。 請注意，一旦刪除並標示為「非作用中」，使用者帳戶就不會再以使用者集合的成員身分傳回（例如，使用[取得客戶的所有使用者帳戶清單](get-a-list-of-all-user-accounts-for-a-customer.md)）。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要還原使用者，請建立[**CustomerUser**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.customeruser)類別的新實例，並將[**user. State**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.user.state)屬性的值設定為[**UserState。 Active**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.userstate)。 將使用者的狀態設定為 [作用中]，以還原已刪除的使用者。 請注意，您不需要重新填入使用者資源中的其餘欄位。 這些值會自動從已刪除的非作用中使用者資源還原。 接下來，使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶，並使用[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法來識別使用者。 最後，呼叫[**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch)方法並傳遞**CustomerUser**實例，以傳送還原使用者的要求。

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

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： CustomerUserRestore.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求語法**

| 方法    | 要求 URI                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **跳** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1。1 |

 

**URI 參數**

使用下列查詢參數來指定客戶識別碼和使用者識別碼。

| 名稱                   | 類型     | 必要項 | 描述                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 此值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商篩選結果給指定的客戶。 |
| **使用者識別碼**            | **guid** | Y        | 值是屬於單一使用者帳戶的 GUID 格式**使用者識別碼**。                                         |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

下表描述要求主體中的必要屬性。

| 名稱       | 類型   | 必要項 | 描述                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| 狀態      | string | Y        | 使用者狀態。 若要還原已刪除的使用者，這必須包含 "active"。 |
| 屬性 | object | N        | 包含 "ObjectType"： "CustomerUser"。                                 |

 

**要求範例**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 回應


如果成功，此方法會在回應主體中傳回已還原的使用者資訊。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

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
