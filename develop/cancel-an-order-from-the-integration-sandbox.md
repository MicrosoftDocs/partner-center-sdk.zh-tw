---
title: 從整合沙箱中取消訂單
description: 從整合沙箱帳戶取消訂單。
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 459db3cfb9a85fd2f4a0d32b065d6929ab40006b
ms.sourcegitcommit: 99fa2c7669f3db84fd00cb5f28ef8d783900c8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84121228"
---
# <a name="cancel-an-order-from-the-integration-sandbox"></a>從整合沙箱中取消訂單

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何從整合沙箱帳戶取消保留實例、軟體和商業 marketplace 軟體即服務（SaaS）訂閱訂單。

>[!NOTE]
>請注意，您只能從整合沙箱帳戶進行保留實例或商業 marketplace SaaS 訂閱訂單的取消。  

若要透過 API 取消軟體的生產訂單，請使用 [[取消]-[軟體-購買](cancel-software-purchases.md)]。
您也可以使用 [[取消購買](https://docs.microsoft.com/partner-center/csp-software-subscriptions.md)]，透過儀表板取消軟體的生產訂單。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 具有使用中保留實例/軟體/協力廠商 SaaS 訂閱訂單之客戶的整合沙箱合作夥伴帳戶。

## <a name="c"></a>C\#

若要取消整合沙箱中的訂單，請將您的帳號憑證傳遞至 [**`CreatePartnerOperations`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) 方法，以取得 [**`IPartner`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner) 介面來取得夥伴作業。

若要選取特定的[訂單](order-resources.md#order)，請使用夥伴作業和呼叫 [**`Customers.ById()`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法搭配客戶識別碼來指定客戶，並在後面加上 **`Orders.ById()`** order identifier 來指定訂單，最後 **`Get`** 或 **`GetAsync`** 方法來取得此順序。

將 [**`Order.Status`**](order-resources.md#order) 屬性設定為 `cancelled` ，並使用 **`Patch()`** 方法來更新順序。

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
| **跳** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來刪除客戶。

| 名稱                   | 類型     | 必要 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。 |
| **訂單識別碼** | **string** | Y        | 值是表示需要取消之訂單識別碼的字串。 |

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
