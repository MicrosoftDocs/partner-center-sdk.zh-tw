---
title: 取得訂用帳戶的佈建狀態
description: 如何取得客戶訂用帳戶的訂用帳戶布建狀態。
ms.assetid: CC3A13FE-D6D3-4A65-981F-0235A4A8382E
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b2be10aea196d4f4049d3f2055709dbc8a5e8eb3
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157210"
---
# <a name="get-subscription-provisioning-status"></a>取得訂用帳戶的佈建狀態

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何取得客戶訂用帳戶的訂用帳戶布建狀態。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 訂用帳戶識別碼。

- 需要訂用帳戶的委派系統管理員許可權，才能執行此作業。

## <a name="c"></a>C\#

若要取得訂用帳戶的布建狀態，請先使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶。 然後，使用訂用帳戶 ID 呼叫[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法，以取得訂用帳戶作業的介面。 接下來，使用[**ProvisioningStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus)屬性來取得目前訂用帳戶布建狀態作業的介面，然後呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync)方法來取出[**SubscriptionProvisioningStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus)物件。

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

使用下列路徑參數來識別客戶和訂用帳戶。

| 名稱            | 類型   | 必要 | 描述                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| customer-id     | 字串 | 是      | 識別客戶的 GUID 格式字串。     |
| subscription-id | 字串 | 是      | 識別訂用帳戶的 GUID 格式字串。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a>備註

- 在基座變更指派期間， [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus)中的 [狀態] 欄位會設定為 [擱置]。

- [狀態] 欄位會每十五分鐘更新一次。
