---
title: 更新購物車
description: 如何更新購物車中的客戶訂單。
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f58aaef8f61deaa17e178b9196f644f9d45137ec
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415025"
---
# <a name="update-a-cart"></a>更新購物車


**適用於**

- 夥伴中心


如何更新購物車中的客戶訂單。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- 現有購物車的購物車識別碼。


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要更新客戶的訂單，請使用**get （）** 方法來取得購物車，其方式是使用**ById （）** 函數傳遞客戶和購物車識別碼。 對購物車進行必要的變更。 現在使用客戶和購物車識別碼，透過**ById （）** 方法來呼叫**Put**方法。

最後，呼叫**Put （）** 或**PutAsync （）** 方法來建立訂單。



``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求語法**

| 方法  | 要求 URI                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1。1              |

 

**URI 參數**

使用下列 path 參數來識別客戶，並指定要更新的購物車。

| 名稱            | 類型     | 必要項 | 描述                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **客戶識別碼** | string   | 是      | 識別客戶的 GUID 格式客戶識別碼。             |
| **購物車-識別碼**     | string   | 是      | 可識別購物車的 GUID 格式的購物車識別碼。                     |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

下表描述要求主體中的[購物車](cart-resources.md)屬性。

| 屬性              | 類型             | 必要項        | 描述                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | 否              | 成功建立購物車時所提供的購物車識別碼。                                  |
| creationTimeStamp     | DateTime         | 否              | 購物車的建立日期（以日期時間格式）。 已在成功建立購物車時套用。        |
| lastModifiedTimeStamp | DateTime         | 否              | 購物車上次更新的日期（以日期時間格式）。 已在成功建立購物車時套用。    |
| expirationTimeStamp   | DateTime         | 否              | 購物車將到期的日期，以日期時間格式為限。  已在成功建立購物車時申請。            |
| lastModifiedUser      | string           | 否              | 上次更新購物車的使用者。 已在成功建立購物車時申請。                             |
| lineItems             | 物件的陣列 | 是             | [CartLineItem](cart-resources.md#cartlineitem)資源的陣列。                                               |


下表描述要求主體中的[CartLineItem](cart-resources.md#cartlineitem)屬性。

| 屬性             | 類型                        | 必要項     | 描述                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | string                      | 否           | 購物車明細專案的唯一識別碼。 已在成功建立購物車時申請。                |
| catalogId            | string                      | 是          | 目錄專案識別碼。                                                                       |
| friendlyName         | string                      | 否           | 選擇性。 由夥伴定義以協助區分的專案易記名稱。              |
| quantity             | int                         | 是          | 授權或實例的數目。     |
| currencyCode         | string                      | 否           | 貨幣代碼。                                                                                 |
| BillingCycle         | 物件                      | 是          | 針對目前期間所設定的計費週期類型。                                              |
| participants         | 物件字串配對的清單 | 否           | 購買的參與者集合。                                                      |
| provisioningCoNtext  | 字典 < 字串，字串 >  | 否           | 用於布建供應專案的內容。                                                          |
| orderGroup           | string                      | 否           | 用來指出哪些專案可以放在一起的群組。                                            |
| 錯誤                | 物件                      | 否           | 在購物車建立後，發生錯誤時套用。                                                 |


**要求範例**

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com 
Content-Length: 496
Expect: 100-continue

{  
    {  
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[  
            {  
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 回應


如果成功，此方法會在回應本文中傳回已填入的[購物車](cart-resources.md)資源。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }            
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```

 

 




