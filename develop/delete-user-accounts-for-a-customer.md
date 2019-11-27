---
title: 刪除客戶的使用者帳戶
description: 如何刪除客戶現有的使用者帳戶。
ms.assetid: 12097809-A62D-4929-9F1D-08676784BA39
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 676865671a4b1fb4512564c7576c39dc6ff4dc73
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486118"
---
# <a name="delete-a-user-account-for-a-customer"></a>刪除客戶的使用者帳戶

適用於：

- 合作夥伴中心

本主題說明如何刪除客戶現有的使用者帳戶。

## <a name="prerequisites"></a>必要條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例僅支援使用應用程式 + 使用者認證進行驗證。
- 客戶識別碼（**客戶租使用者識別碼**）。 如果您沒有客戶的識別碼，請在 [合作夥伴中心] 中查詢識別碼。 從 [customers] 清單中選擇客戶，選取 [**帳戶**]，然後儲存其 Microsoft 識別碼。
- 使用者識別碼。 如果您沒有使用者識別碼，請參閱[取得客戶的所有使用者帳戶清單](get-a-list-of-all-user-accounts-for-a-customer.md)。

## <a name="deleting-a-user-account"></a>刪除使用者帳戶

當您刪除使用者帳戶時，使用者狀態會設定為**非**作用中30天。 三十天后，會清除使用者帳戶及其相關聯的資料，並使其無法復原。

如果非使用中的帳戶在三十天的時間範圍內，您可以[為客戶還原已刪除的使用者帳戶](restore-a-user-for-a-customer.md)。 不過，當您還原已刪除且標示為非使用中的帳戶時，該帳戶將不再以使用者集合的成員身分傳回（例如，當您[取得客戶的所有使用者帳戶清單](get-a-list-of-all-user-accounts-for-a-customer.md)時）。

## <a name="c"></a>C\#

若要刪除現有的客戶使用者帳戶：

1. 使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法搭配客戶識別碼來識別客戶。
2. 呼叫[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法來識別使用者。
3. 呼叫[**delete**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete)方法來刪除使用者，並將使用者狀態設定為非作用中。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： DeleteCustomerUser.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

使用下列查詢參數來識別客戶和使用者。

| 名稱                   | 類型     | 必要 | 描述                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| 客戶-租使用者識別碼     | GUID     | Y        | 此值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商篩選指定客戶的結果。 |
| user-id                | GUID     | Y        | 值是屬於單一使用者帳戶的 GUID 格式**使用者識別碼**。                                          |

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

如果成功，這個方法會傳回**204 沒有內容**狀態碼。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

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
