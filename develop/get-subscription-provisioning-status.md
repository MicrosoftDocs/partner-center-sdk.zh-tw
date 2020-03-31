---
title: 取得訂用帳戶布建狀態
description: 如何取得客戶訂用帳戶的訂用帳戶布建狀態。
ms.assetid: CC3A13FE-D6D3-4A65-981F-0235A4A8382E
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 189ff5d3d452c27e248d4051cfb337c87d4c4d7d
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416641"
---
# <a name="get-subscription-provisioning-status"></a>取得訂用帳戶布建狀態

**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何取得客戶訂用帳戶的訂用帳戶布建狀態。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼。
- 訂用帳戶識別碼。
- 需要訂用帳戶的委派系統管理員許可權，才能執行此作業。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取得訂用帳戶的布建狀態，請先使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶。 然後，使用訂用帳戶 ID 呼叫[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法，以取得訂用帳戶作業的介面。 接下來，使用[**ProvisioningStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus)屬性來取得目前訂用帳戶布建狀態作業的介面，然後呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync)方法來取出[**SubscriptionProvisioningStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus)物件。

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId; 

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求


**要求語法**

| 方法  | 要求 URI                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1。1 |

 

**URI 參數**

使用下列路徑參數來識別客戶和訂用帳戶。

| 名稱            | 類型   | 必要項 | 描述                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| 客戶識別碼     | string | 是      | 識別客戶的 GUID 格式字串。     |
| 訂用帳戶識別碼 | string | 是      | 識別訂用帳戶的 GUID 格式字串。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應主體會包含[SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus)資源。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

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

## <a name="span-idremarksspan-idremarksspan-idremarksremarks"></a><span id="Remarks"/><span id="remarks"/><span id="REMARKS"/>備註

- 在基座變更指派期間， [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus)中的 [狀態] 欄位會設定為 [擱置]。
- [狀態] 欄位會每十五分鐘更新一次。