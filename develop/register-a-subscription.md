---
title: 註冊訂用帳戶
description: 註冊現有的訂用帳戶，以啟用它來排序 Azure 保留。
ms.assetid: 9B853BF2-855C-4EB3-BBE5-7ECC1336AE08
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7e732d058000aa09177d94534ebbe77a05d43bef
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157030"
---
# <a name="register-a-subscription"></a>註冊訂用帳戶

**適用于**

- 合作夥伴中心

註冊現有的[訂](subscription-resources.md)用帳戶，以啟用它來排序 Azure 保留。

若要購買 Azure 保留，您必須至少有一個現有的 CSP Azure 訂用帳戶。 這個方法可讓您註冊現有的 CSP Azure 訂用帳戶，讓它能夠購買 Azure 保留。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 訂用帳戶識別碼。

## <a name="c"></a>C\#

若要註冊客戶的訂用帳戶，請透過呼叫[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶，以取出訂閱作業的介面。 然後，使用訂用帳戶識別碼呼叫[**ById （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)方法，以識別您要註冊的訂用帳戶。

最後，呼叫 register **（）** 方法來註冊訂用帳戶，並取出可用來取得訂用帳戶註冊狀態的 URI。 如需詳細資訊，請參閱[取得訂用帳戶註冊狀態](get-subscription-registration-status.md)。

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
| customer-id             | 字串     | 是      | 識別客戶的 GUID 格式字串。         |
| subscription-id         | 字串     | 是      | 識別訂用帳戶的 GUID 格式字串。     |

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

如果成功，回應會包含具有 URI 的**位置**標頭，可用來抓取訂用帳戶註冊狀態。 儲存此 URI 以與其他相關的 REST Api 搭配使用。 如需如何取得狀態的範例，請參閱[取得訂用帳戶註冊狀態](get-subscription-registration-status.md)。

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
