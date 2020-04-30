---
title: 為客戶更新使用者帳戶
description: 為您的客戶更新現有使用者帳戶中的詳細資料。
ms.assetid: 26E79662-2376-4208-A645-20069DBE0457
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b34ca8a1646470dd53b4e830558cf7edbd2cc644
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157890"
---
# <a name="update-user-accounts-for-a-customer"></a>為客戶更新使用者帳戶

**適用于**

- 合作夥伴中心

為您的客戶更新現有使用者帳戶中的詳細資料。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

## <a name="c"></a>C\#

若要更新指定客戶使用者的詳細資料，請先取出指定的客戶識別碼和使用者以進行更新。 然後，在新的**CustomerUser**物件中建立使用者的更新版本。 然後，使用您的**iaggregatepartner.customers.byid**集合並呼叫**ById （）** 方法。 然後呼叫**Users**屬性、 **ById （）** 方法，後面接著**Patch （）** 方法。

``` csharp
// string selectedCustomerId;
// customerUser specifiedUser;
// IAggregatePartner partnerOperations;

// Updated information
var userToUpdate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "testPw@!122B" },
    DisplayName = "DisplayNameChange",
    FirstName = "FirstNameChange",
    LastName = "LastNameChange",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

// Update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSamples**類別**： CustomerUserUpdate.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| **跳** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來識別正確的客戶。

| 名稱                   | 類型     | 必要 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。 |
| **使用者識別碼**            | **guid** | Y        | 值是屬於單一使用者帳戶的 GUID 格式**使用者識別碼**。                                                                       |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

### <a name="request-example"></a>要求範例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "new country/region code",

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回具有更新資訊的使用者帳戶。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "new country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "emailidchange@abcdefgh1234.ccsctp.net",
  "firstName": "FirstNameChange",
  "lastName": "LastNameChange",
  "displayName": "DisplayNameChange",
  "userDomainType": "none",
  "state": "active",
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/4b10bf41-ab11-40e3-8c53-cd67849b50de",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
