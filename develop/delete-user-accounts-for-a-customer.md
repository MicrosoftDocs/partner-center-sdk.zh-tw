---
title: 為客戶刪除使用者帳戶
description: 如何刪除客戶現有的使用者帳戶。
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927807"
---
# <a name="delete-a-user-account-for-a-customer"></a>為客戶刪除使用者帳戶

**適用於：**

- 合作夥伴中心

本文說明如何刪除客戶現有的使用者帳戶。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 使用者 ID。 如果您沒有使用者識別碼，請參閱 [取得客戶的所有使用者帳戶清單](get-a-list-of-all-user-accounts-for-a-customer.md)。

## <a name="deleting-a-user-account"></a>刪除使用者帳戶

當您刪除使用者帳戶時，使用者狀態會設定為 [ **非** 使用中] 30 天。 30天后，就會清除使用者帳戶及其相關聯的資料，並使其無法復原。

如果非使用中帳戶是在三十天的時間範圍內，您可以 [為客戶還原已刪除的使用者帳戶](restore-a-user-for-a-customer.md) 。 但是，當您還原已刪除並標示為非使用中的帳戶時，該帳戶就不會再以使用者集合的成員形式傳回 (例如，當您 [取得客戶) 的所有使用者帳戶清單](get-a-list-of-all-user-accounts-for-a-customer.md) 時。

## <a name="c"></a>C\#

若要刪除現有的客戶使用者帳戶：

1. 使用 [**>iaggregatepartner.customers. >iaggregatepartner.customers.byid**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法搭配客戶識別碼來識別客戶。

2. 呼叫 [**>iaggregatepartner.customers.byid**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) 方法來識別使用者。

3. 呼叫 [**delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) 方法來刪除使用者，並將使用者狀態設為非作用中。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： DeleteCustomerUser.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| 刪除     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

使用下列查詢參數來識別客戶和使用者。

| 名稱                   | 類型     | 必要 | 說明                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| customer-tenant-id     | GUID     | Y        | 此值是 GUID 格式的 **客戶租使用者識別碼** ，可讓轉銷商篩選指定客戶的結果。 |
| user-id                | GUID     | Y        | 此值是屬於單一使用者帳戶的 GUID 格式 **使用者識別碼** 。                                          |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回 **204 沒有內容** 狀態碼。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
