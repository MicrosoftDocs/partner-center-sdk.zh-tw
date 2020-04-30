---
title: 取得客戶清單
description: 如何取得代表合作夥伴所有客戶的資源集合。
ms.assetid: 6D636257-7C23-4DDF-9895-96F208B66232
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 8f1115385ad020f8a7c20810765842e19dd53cd1
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156880"
---
# <a name="get-a-list-of-customers"></a>取得客戶清單

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本文說明如何取得代表合作夥伴所有客戶的資源集合。

> [!TIP]
> 您也可以在合作夥伴中心儀表板中執行此操作。 在主頁面的 [**客戶管理**] 底下，選取 [ **View Customers**]。 或者，在提要欄位上選取 [**客戶**]。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

## <a name="c"></a>C\#

若要取得所有客戶的清單：

1. 使用[**iaggregatepartner.customers.byid. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers)集合來建立**ipartner.getinvoices**物件。

2. 使用[**Query （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query)或[**QueryAsync （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)方法來取出客戶清單。 （如需有關建立查詢的指示，請參閱[**QueryFactory**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)類別）。

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

如需範例，請參閱下列各項：

- 範例：[主控台測試應用程式](console-test-app.md)
- 專案： **PartnerSDK. FeatureSamples**
- 類別： **CustomerPaging.cs**

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要取得所有客戶的清單：

1. 使用 [**Iaggregatepartner.customers.byid getCustomers**] 函數來取得客戶作業的參考。

2. 使用**query （）** 函數來抓取客戶清單。

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

執行不含參數的[**PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md)命令，以取得完整的客戶清單。

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                   |
|---------|-------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers？ size = {SIZE} HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來取得客戶的清單。

| 名稱     | 類型    | 必要 | 描述                                        |
|----------|---------|----------|----------------------------------------------------|
| **size** | **int** | Y        | 要一次顯示的結果數目。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回[客戶](customer-resources.md#customer)資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
