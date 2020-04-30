---
title: 取得訂用帳戶的註冊狀態
description: 取得已註冊使用 Azure 保留的 VM 執行個體之訂用帳戶的狀態。
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 86c7254876110a5f5b03317c7cd79a23d1f63332
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157200"
---
# <a name="get-subscription-registration-status"></a>取得訂用帳戶的註冊狀態

**適用于**

- 合作夥伴中心

如何取得已啟用購買 Azure 保留的 VM 執行個體之客戶訂用帳戶的訂用帳戶註冊狀態。

若要使用合作夥伴中心 API 購買 Azure 保留的 VM 實例，您必須至少有一個現有的 CSP Azure 訂用帳戶。 [註冊訂用](register-a-subscription.md)帳戶方法可讓您註冊現有的 CSP Azure 訂用帳戶，讓它能夠 Azure 保留的 VM 執行個體購買。 這個方法可讓您取得該註冊的狀態。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 訂用帳戶識別碼。

## <a name="c"></a>C\#

若要取得訂用帳戶的註冊狀態，請先使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶。 然後，藉由呼叫[**ById （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)方法與訂用帳戶識別碼來取得訂用帳戶作業的介面，以識別訂用帳戶。 接下來，使用 RegistrationStatus 屬性來取得目前訂用帳戶註冊狀態作業的介面，並呼叫**Get**或**GetAsync**方法來取出**SubscriptionRegistrationStatus**物件。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

使用下列路徑參數來識別客戶和訂用帳戶。

| 名稱                    | 類型       | 必要 | 描述                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| customer-id             | 字串     | 是      | 識別客戶的 GUID 格式字串。         |
| subscription-id         | 字串     | 是      | 識別訂用帳戶的 GUID 格式字串。     |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
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

如果成功，回應主體會包含[SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
