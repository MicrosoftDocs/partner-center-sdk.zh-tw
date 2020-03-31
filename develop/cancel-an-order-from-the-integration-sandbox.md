---
title: 從整合沙箱取消訂單
description: 從整合沙箱帳戶取消訂單。
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 4e3aa651731b4cf624d1266e3c780e2acbb9c0d4
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413090"
---
# <a name="cancel-an-order-from-the-integration-sandbox"></a>從整合沙箱取消訂單

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何從整合沙箱帳戶取消保留實例、軟體和商業 marketplace 軟體即服務（SaaS）訂閱訂單。

>[!NOTE]
>請注意，只有整合沙箱帳戶才能取消保留實例、軟體或商用 marketplace SaaS 訂閱訂單。 若要取消生產訂單，請洽詢合作夥伴中心支援。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 整合沙箱合作夥伴帳戶，具有具有使用中保留實例/軟體/協力廠商 SaaS 訂閱訂單的客戶。

## <a name="c"></a>C#

若要取消整合沙箱中的訂單，請將您的帳號憑證傳遞至[**CreatePartnerOperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.partnerservice.instance)方法，以取得[**ipartner.getinvoices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner)介面來取得夥伴作業。

若要選取特定[訂單](order-resources.md#order)，請使用交易夥伴作業並呼叫[**ById （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，並使用客戶識別碼來指定客戶，後面接著**ById （）** 與訂單識別碼，以指定訂單，最後**取得**或**GetAsync**方法來取得該順序。

將 [[**順序**](order-resources.md#order)] 屬性設定為 [已取消]，並使用**Patch （）** 方法來更新順序。

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **跳** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來刪除客戶。

| 名稱                   | 類型     | 必要項 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。 |
| **訂單識別碼** | **字串** | Y        | 值為字串，表示需要取消的訂單識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文
```http
{  
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",  
    "status": "cancelled",  
}
```

### <a name="request-example"></a>要求範例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回已取消的順序。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
