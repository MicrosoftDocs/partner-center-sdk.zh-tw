---
title: 取消購買軟體
description: 使用合作夥伴中心 Api 取消軟體訂閱和永久軟體購買的自助選項。
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1da4e45bcfa3c54316139fefa348044643256190
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413047"
---
# <a name="cancel-software-purchases"></a>取消購買軟體

適用於：

- 夥伴中心

您可以使用合作夥伴中心 Api，從購買日期取消軟體訂閱和永久軟體購買。 您不需要建立支援票證來進行這類取消，而可以改為使用下列自助服務方法。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

## <a name="c"></a>C\#

若要取消軟體訂單，

1. 將您的帳號憑證傳遞至[**CreatePartnerOperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.partnerservice.instance)方法，以取得[**ipartner.getinvoices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner)介面來取得合作夥伴作業。

2. 選取您想要取消的特定[訂單](order-resources.md#order)。 使用客戶識別碼呼叫[**ById （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，後面接著**ById （）** 與訂單識別碼。

3. 呼叫**Get**或**GetAsync**方法以取得訂單。

4. 將[**Order. Status**](order-resources.md#order)屬性設為「已取消」。

5. 選擇性如果您想要指定取消的特定行專案，請將[**LineItems**](order-resources.md#order)設定為您要取消之行專案的清單。

6. 使用**Patch （）** 方法來更新訂單。

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **跳** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

使用下列查詢參數來刪除客戶。

| 名稱                   | 類型     | 必要項 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 此值是 GUID 格式的客戶租使用者識別碼，可讓轉銷商針對屬於轉售商的特定客戶篩選其結果。 |
| **訂單識別碼** | **字串** | Y        | 值為字串，表示您想要取消之訂單的識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a>要求範例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回具有已取消之明細專案的順序。

訂單狀態會標示為 [已**取消**] （如果訂單中的所有明細專案已取消）或 [**已完成**] （如果未取消訂單中的所有明細專案）。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

在下列範例回應中，您可以看到具有供應專案識別碼**DG7GMGF0FKZV：0003： DG7GMGF0DWMS**的明細專案數量已變成零（0）。 這項變更表示已成功取消標示為取消的行專案。 範例順序包含其他未取消的明細專案，這表示整體訂單的狀態會標示為**已完成**，而不是**取消**。

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
