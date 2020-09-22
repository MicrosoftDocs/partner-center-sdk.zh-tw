---
title: 更新訂用帳戶的支援連絡人
description: 如何將訂用帳戶的支援連絡人更新為合作夥伴的其中一個增值轉銷商。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 39275394b2fecd67a25c9315ed11b9333532f514
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925442"
---
# <a name="update-a-subscriptions-support-contact"></a>更新訂用帳戶的支援連絡人

**適用於**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何將訂用帳戶的支援連絡人更新為合作夥伴的其中一個增值轉銷商。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 訂用帳戶識別碼。

- 新支援連絡人的相關資訊：租使用者識別碼、Microsoft 合作夥伴網路識別碼和名稱。 支援連絡人必須是合作夥伴的其中一個增值轉銷商。

## <a name="c"></a>C\#

若要更新訂用帳戶的支援連絡人，請先具現化，並以新的值填入 [**SupportContact**/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) 物件。 然後，搭配客戶識別碼使用 [**>iaggregatepartner.customers. >iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法來識別客戶。 接下來，使用訂用帳戶識別碼呼叫 [**>iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) 方法，以取得訂用帳戶作業的介面。 然後，使用 [**SupportContact**/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) 屬性來取得支援連絡人作業的介面。 最後，使用填入的 SupportContact 物件來呼叫 [**update**/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) 或 [**>updateasync**/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync]) 方法，以更新支援連絡人。

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： UpdateSubscriptionSupportContact.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列路徑參數來識別客戶和訂用帳戶。

| 名稱            | 類型   | 必要 | 描述                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| customer-id     | 字串 | Yes      | 可識別客戶的 GUID 格式字串。           |
| subscription-id | 字串 | Yes      | GUID 格式的字串，可識別試用版訂用帳戶。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

您必須在要求主體中包含已填入的 [SupportContact](subscription-resources.md#supportcontact) 資源。 支援連絡人必須是具有合作夥伴關係的現有轉銷商。

### <a name="request-example"></a>要求範例

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含 [SupportContact](subscription-resources.md#supportcontact) 資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
