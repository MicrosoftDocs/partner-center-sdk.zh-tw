---
title: 註冊訂用帳戶
description: 註冊現有的訂用帳戶，以啟用 Azure 保留的訂購。
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3cabfd9d2bba309d773f15b2de2a4b33e4575241
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926661"
---
# <a name="register-a-subscription"></a>註冊訂用帳戶

**適用於**

- 合作夥伴中心

註冊現有的 [訂](subscription-resources.md) 用帳戶，以啟用 Azure 保留的訂購。

若要購買 Azure 保留，您必須至少有一個現有的 CSP Azure 訂用帳戶。 此方法可讓您註冊現有的 CSP Azure 訂用帳戶，以便購買 Azure 保留。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 訂用帳戶識別碼。

## <a name="c"></a>C\#

若要註冊客戶的訂用帳戶，請使用客戶識別碼呼叫 [**>iaggregatepartner.customers >iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法來取得訂用帳戶作業的介面，以識別客戶。 然後，使用訂用帳戶識別碼來呼叫 [**>iaggregatepartner.customers.byid ( # B1 **/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) 方法，以識別您要註冊的訂用帳戶。

最後，呼叫 **註冊。註冊 ( # B1 ** 方法以註冊訂用帳戶，並取得可用來取得訂用帳戶註冊狀態的 URI。 如需詳細資訊，請參閱 [取得訂用帳戶註冊狀態](get-subscription-registration-status.md)。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

使用下列路徑參數來識別客戶和訂用帳戶。

| 名稱                    | 類型       | 必要 | 描述                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| customer-id             | 字串     | Yes      | 可識別客戶的 GUID 格式字串。         |
| subscription-id         | 字串     | Yes      | 識別訂用帳戶的 GUID 格式字串。     |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，回應會包含具有 URI 的 **Location** 標頭，可用來取得訂用帳戶註冊狀態。 儲存此 URI 以搭配其他相關 REST Api 使用。 如需如何取得狀態的範例，請參閱 [取得訂用帳戶註冊狀態](get-subscription-registration-status.md)。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
