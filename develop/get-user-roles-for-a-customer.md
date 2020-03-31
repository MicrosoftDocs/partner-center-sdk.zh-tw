---
title: 為客戶取得使用者角色
description: 取得附加至使用者帳戶的所有角色/許可權清單。 變化包括取得客戶所有使用者帳戶的擁有權限清單，以及取得具有指定角色的使用者清單。
ms.assetid: 304A1C1F-6280-40E9-A96B-F87ECA657FF3
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 97c377d3a21fe6123a743ec1878f28b0fab719b2
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416562"
---
# <a name="get-user-roles-for-a-customer"></a>為客戶取得使用者角色


**適用於**

- 夥伴中心

取得附加至使用者帳戶的所有角色/許可權清單。 變化包括取得客戶所有使用者帳戶的擁有權限清單，以及取得具有指定角色的使用者清單。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取得指定客戶的所有目錄角色，請先取出指定的客戶識別碼。 然後，使用您的**iaggregatepartner.customers.byid**集合並呼叫**ById （）** 方法。 然後呼叫**DirectoryRoles**屬性，後面接著**Get （）** 或<strong>GetAsync （）</strong>方法。

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： GetCustomerDirectoryRoles.cs

若要取得具有指定角色的客戶使用者清單，請先取出指定的客戶識別碼和目錄角色識別碼。 然後，使用您的**iaggregatepartner.customers.byid**集合並呼叫**ById （）** 方法。 然後呼叫**DirectoryRoles**屬性、 **ById （）** 方法、 **UserMembers**屬性、後面接著**Get （）** 或<strong>GetAsync （）</strong>方法。

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSamples**類別**： GetCustomerDirectoryRoleUserMembers.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求語法**

| 方法  | 要求 URI                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1。1 |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1。1                 |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers    |

 

**URI 參數**

使用下列查詢參數來識別正確的客戶。

| 名稱                   | 類型     | 必要項 | 描述                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。                                                      |
| **使用者識別碼**            | **guid** | N        | 值是屬於單一使用者帳戶的 GUID 格式**使用者識別碼**。                                                                                                                            |
| **角色識別碼**            | **guid** | N        | 值是屬於某個角色類型的 GUID 格式**角色識別碼**。 您可以在所有使用者帳戶中查詢客戶的所有目錄角色，以取得這些識別碼。 （上述的第二個案例）。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 回應


如果成功，這個方法會傳回與指定的使用者帳戶相關聯的角色清單。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```