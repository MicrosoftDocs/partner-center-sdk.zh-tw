---
title: 取得客戶的服務成本明細專案
description: 取得指定計費期間的客戶服務成本明細專案。
ms.assetid: 1D6364A2-51FE-44E4-96A0-444EDB3BB56A
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 67e6c803995759942748aac79473911b2aa2f9e7
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80070120"
---
# <a name="get-a-customers-service-costs-line-items"></a>取得客戶的服務成本明細專案

適用於：

- 夥伴中心

取得指定計費期間的客戶服務成本明細專案。

## <a name="prerequisites"></a>必要條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用應用程式加上使用者的認證來進行驗證。
- 客戶識別碼。
- 計費週期指標（**mostrecent**）。

## <a name="c"></a>C\#

若要取得指定客戶的服務成本摘要：

1. 使用客戶識別碼呼叫[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，以識別客戶。
2. 使用[**ServiceCosts**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts)屬性來取得客戶服務成本集合作業的介面。
3. 呼叫具有[**ServiceCostsBillingPeriod**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod)列舉成員的[**ByBillingPeriod**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod)方法，以傳回[**iservicecostscollection 請使用**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)。
4. 使用[**iservicecostscollection 請使用. LineItems. get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync)方法來取得客戶的服務成本明細專案。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

使用下列路徑參數來識別客戶和計費期間。

| 名稱           | 類型   | 必要項 | 描述                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| 客戶識別碼    | guid   | 是      | 識別客戶的 GUID 格式客戶識別碼。                                                                       |
| 計費-期間 | string | 是      | 表示計費週期的指標。 唯一支援的值為 MostRecent。 字串的大小寫並不重要。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

None。

### <a name="request-example"></a>要求的範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[ServiceCostLineItem](service-costs-resources.md)資源，以提供服務成本的相關資訊。

> [!IMPORTANT]
> 下列屬性*僅適用于*產品為*一次性購買*的服務成本明細專案： **productId**、 **productName**、 **skuId**、 **skuName**、 **availabilityId**、 **publisherId**、 **publisherName**、 **termAndBillingCycle**、 **discountDetails**。 這些屬性不適*用於*產品為*週期性購買*的服務明細專案。 例如，這些屬性*不適*用於以訂用帳戶為基礎的 Office 365 和 Azure。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 2148
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "attributes": {
        "objectType": "Collection"
    },
    "items":
    [{
            "afterTaxTotal": 0.0,
            "chargeType": "PURCHASE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-01-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 0.0,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2015-12-15T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 0.0,
            "invoiceNumber": "T000003163",
            "invoiceType": "OneTime",
            "productId": "DZH318Z0BJR6",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BMFK",
            "productName": "Azure Managed Experience",
            "skuName": "Azure Managed Experience - Optimize",
            "publisherName": "Microsoft",
            "publisherId": "01323244",
            "termAndBillingCycle": "",
            "discountDetails": "N/A"
        }, {
            "afterTaxTotal": 17.219999999999999,
            "chargeType": "CYCLE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-02-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 17.219999999999999,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2016-01-12T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 17.219999999999999,
            "invoiceNumber": "D000003163",
            "invoiceType": "Recurring",
            "productId": "DZH318Z0BJR7",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BTTTT",
            "productName": "NGINX Plus",
            "skuName": "NGINX Plus (Ubuntu 14.04)",
            "publisherName": "Nginx, Inc.",
            "publisherId": "212336222",
            "termAndBillingCycle": "30 Days Trial",
            "discountDetails": "20%"
        }
    ],
    "links": {
        "self": {
            "headers": [],
            "method": "GET",
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems"
        }
    },
    "totalCount": 2
}
```
