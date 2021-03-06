---
title: 依照識別碼取得訂單
description: 取得符合客戶和訂單識別碼的訂單資源。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8911adba28836aa378260d8b61e2b6e23eabc096
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927136"
---
# <a name="get-an-order-by-id"></a>依照識別碼取得訂單

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得符合客戶和訂單識別碼的 [訂單](order-resources.md) 資源。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 訂單識別碼。

## <a name="c"></a>C\#

若要取得客戶的訂單（依識別碼）：

1. 使用您的 **>iaggregatepartner.customers. Customers** 集合，並呼叫 **>iaggregatepartner.customers.byid ( # B1 ** 方法。

2. 呼叫 [**Orders**/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) 屬性，後面接著 [**>iaggregatepartner.customers.byid ( # B2 **/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) 方法。
3. 呼叫 [**Get ( # B1 **/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) 或 [**GetAsync ( # B4 **/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync) 。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSample **類別**： GetOrder.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要取得客戶的訂單（依識別碼）：

1. 使用您的 **>iaggregatepartner.customers getCustomers** 函數，然後呼叫 **>iaggregatepartner.customers.byid ( # B1 ** 函數。

2. 呼叫 **getOrders** 函式，後面接著 **>iaggregatepartner.customers.byid ( # B1 ** 函數。
3. 呼叫 **get ( # B1 ** 函數。

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

若要依識別碼取得客戶的訂單，請執行 [**PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) 命令，並指定 **CustomerId** 和 **訂單** 識別碼參數。

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1。1  |

#### <a name="uri-parameters"></a>URI 參數

下表列出可依識別碼取得訂單的必要查詢參數。

| 名稱                   | 類型     | 必要 | 說明                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| customer-tenant-id     | 字串   | Yes      | 對應至客戶的 GUID 格式字串。 |
| id-for-order           | 字串   | Yes      | 對應至訂單識別碼的字串。                |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回 [訂單](order-resources.md) 資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
