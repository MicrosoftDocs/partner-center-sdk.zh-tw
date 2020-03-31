---
title: 依 ID 取得訂用帳戶
description: 取得符合客戶識別碼和訂用帳戶識別碼的訂用帳戶資源。
ms.assetid: 0A91755F-C5AB-4CB1-9E61-6C927F6AA5C5
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcb867455b2f0c67f294ac2de54d7b2ad52c1231
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416802"
---
# <a name="get-a-subscription-by-id"></a>依 ID 取得訂用帳戶


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得符合客戶識別碼和訂用帳戶識別碼的[訂](subscription-resources.md)用帳戶資源。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- 訂用帳戶識別碼。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要依識別碼取得訂用帳戶，請從取得訂閱作業的介面開始，方法是呼叫[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來識別客戶，並使用[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法來識別訂用帳戶。 使用該[**介面**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription)，藉由呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)來抓取訂用帳戶詳細資料。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionID;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionID).Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： GetSubscription.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法  | 要求 URI                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1。1 |

 

**URI 參數**

下表列出取得訂用帳戶所需的查詢參數。

| 名稱                    | 類型     | 必要項 | 描述                               |
|-------------------------|----------|----------|-------------------------------------------|
| **客戶-租使用者識別碼**  | **guid** | Y        | 對應至客戶的 GUID。     |
| **訂用帳戶的識別碼** | **guid** | Y        | 對應至訂用帳戶的 GUID。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99 HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，此方法會在回應主體中傳回[訂](subscription-resources.md)用帳戶資源。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**標準訂用帳戶的回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 833
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CV: 7v11Wa//5EuGEo+A.0
MS-ServerId: 202010406
Date: Fri, 27 Jan 2017 21:51:40 GMT

{
    "id": "A356AC8C-E310-44F4-BF85-C7F29044AF99", 
    "entitlementId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
    "offerId": "MS-AZR-0145P",
    "offerName": "Microsoft Azure",
    "friendlyName": "Microsoft Azure",
    "quantity": 1,
    "unitType": "Usage-based",
    "creationDate": "2016-05-10T07:30:05.427Z",
    "effectiveStartDate": "2016-05-10T00:00:00Z",
    "commitmentEndDate": "9999-12-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": false,
    "billingType": "usage",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/MS-AZR-0145P?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "B23FDEDD-D6BD-415A-8B71-3624C81C9644",
    "attributes": {
        "etag": "eyJpZCI6ImEzNTZhYzhjLWUzMTAtNDRmNC1iZjg1LWM3ZjI5MDQ0YWY5OSIsInZlcnNpb24iOjJ9",
        "objectType": "Subscription"
    }
}
```

**附加元件訂用帳戶的回應範例**

附加元件訂用帳戶的回應包括主體中的父訂用帳戶識別碼，以及連結中的。

```http
HTTP/1.1 200 OK
Content-Length: 1132
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6eacec93-852d-4167-9d96-c57809bea7ed
MS-RequestId: 22bfd0fb-d1e6-4a8f-aa1a-124b7c820d80
MS-CV: cmde2DtbuUWi8JLq.0
MS-ServerId: 201022015
Date: Fri, 27 Jan 2017 00:12:53 GMT

{
    "id": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
    "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
    "offerName": "Exchange Online Archiving for Exchange Online",
    "friendlyName": "Some friendly name",
    "quantity": 2,
    "unitType": "Licenses",
    "parentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
    "creationDate": "2017-01-25T23:01:08.693Z",
    "effectiveStartDate": "2017-01-25T00:00:00Z",
    "commitmentEndDate": "2018-02-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": true,
    "billingType": "license",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60?country=US",
            "method": "GET",
            "headers": []
        },
        "parentSubscription": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "CF3B0E37-BE0B-4CDD-B584-D1A97D98A922",
    "attributes": {
        "etag": "eyJpZCI6Ijk2OGJhMWNmLWMxNDYtNGFkZi1hMzAwLTMwOGRjZjcxOGVlZSIsInZlcnNpb24iOjF9",
        "objectType": "Subscription"
    }
}
```

 

 




