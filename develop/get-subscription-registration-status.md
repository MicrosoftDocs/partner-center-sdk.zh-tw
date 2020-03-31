---
title: 取得訂用帳戶註冊狀態
description: 取得已註冊使用 Azure 保留的 VM 執行個體之訂用帳戶的狀態。
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0671ab9bfc9bf254a9bc5472c4ed0f65153af1af
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416628"
---
# <a name="get-subscription-registration-status"></a>取得訂用帳戶註冊狀態 

**適用於**

- 夥伴中心

如何取得已啟用購買 Azure 保留的 VM 執行個體之客戶訂用帳戶的訂用帳戶註冊狀態。  

若要使用合作夥伴中心 API 購買 Azure 保留的 VM 實例，您必須至少有一個現有的 CSP Azure 訂用帳戶。 [註冊訂用](register-a-subscription.md)帳戶方法可讓您註冊現有的 CSP Azure 訂用帳戶，讓它能夠 Azure 保留的 VM 執行個體購買。 這個方法可讓您取得該註冊的狀態。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- 訂用帳戶識別碼。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取得訂用帳戶的註冊狀態，請先使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶。 然後，藉由呼叫[**ById （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)方法與訂用帳戶識別碼來取得訂用帳戶作業的介面，以識別訂用帳戶。 接下來，使用 RegistrationStatus 屬性來取得目前訂用帳戶註冊狀態作業的介面，並呼叫**Get**或**GetAsync**方法來取出**SubscriptionRegistrationStatus**物件。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求

**要求語法**

| 方法    | 要求 URI                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1。1 |

**URI 參數**

使用下列路徑參數來識別客戶和訂用帳戶。 

| 名稱                    | 類型       | 必要項 | 描述                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| 客戶識別碼             | string     | 是      | 識別客戶的 GUID 格式字串。         |
| 訂用帳戶識別碼         | string     | 是      | 識別訂用帳戶的 GUID 格式字串。     |

 
**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

None。

**要求範例**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 回應

如果成功，回應主體會包含[SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus)資源。  

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

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