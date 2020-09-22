---
title: 依照訂單明細項目取得啟用連結
description: 依訂單明細專案取得訂用帳戶啟用連結。
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c0e84888870571cf6bd21306f527863f2aa7ee85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927231"
---
# <a name="get-activation-link-by-order-line-item"></a>依照訂單明細項目取得啟用連結

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

依訂單明細專案編號取得商業 marketplace 訂用帳戶啟用連結。

在 [合作夥伴中心儀表板] 中，您可以在主頁面上選取 [**訂**用帳戶] 下的**特定訂**用帳戶，或在 [**訂閱**] 頁面上選取要啟用之訂閱旁的 [**移至發行者的網站**] 連結，來執行這項作業。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 需要啟用的產品已完成訂單。

## <a name="c"></a>C\#

若要取得明細專案的啟用連結，請使用您的 [**>iaggregatepartner.customers. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) 集合，並使用選取的客戶識別碼來呼叫 [**>iaggregatepartner.customers.byid ( # B1 **](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法。 然後以您指定的[**訂單 id**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id)，呼叫[**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)屬性和[**>iaggregatepartner.customers.byid ( # B1**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)方法。 然後，使用具有明細專案編號識別碼的 **>iaggregatepartner.customers.byid ( # B1**方法來呼叫[**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) 。  最後，呼叫 **ActivationLinks ( # B1 ** 方法。

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應本文中傳回 [客戶](customer-resources.md#customer) 資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
