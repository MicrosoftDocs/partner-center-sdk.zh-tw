---
title: 從角色中移除客戶使用者
description: 如何從客戶帳戶中的目錄角色移除使用者。
ms.assetid: 5129AB77-0A66-47A3-8DE8-1AC23C53F81A
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e5ad5d6c592b0e0d576cf9f84f04ee40336b3680
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157010"
---
# <a name="remove-a-customer-user-from-a-role"></a>從角色中移除客戶使用者

**適用于**

- 合作夥伴中心

如何從客戶帳戶中的目錄角色移除使用者。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

## <a name="c"></a>C\#

若要從目錄角色中移除使用者，請選取要使用[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法的呼叫來修改使用者的客戶，並在該處以[**DirectoryRoles. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid)方法指定角色，並搭配目錄角色識別碼。 然後，存取[**UserMembers. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid)方法來識別要移除的使用者，並使用[**Delete**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete)方法從角色中移除使用者。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： RemoveCustomerUserMemberFromDirectoryRole.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **DELETE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列 URI 參數來識別正確的客戶、角色和使用者。

| 名稱                   | 類型     | 必要 | 描述                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 此值是可識別客戶的 GUID 格式**客戶租使用者識別碼**。 |
| **角色識別碼**            | **guid** | Y        | 值是可識別角色的 GUID 格式**角色識別碼**。                |
| **使用者識別碼**            | **guid** | Y        | 此值是可識別單一使用者帳戶的 GUID 格式**使用者識別碼**。   |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功地從角色中移除使用者，回應主體會是空的。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
