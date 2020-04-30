---
title: 取得產品清單 (以國家/地區為基礎)
description: 您可以使用產品資源來取得依客戶國家/地區的產品集合。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7427c3b3f28ac3cd6a2694fe90ac9024f913c749
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156900"
---
# <a name="get-a-list-of-products-by-country"></a>取得產品清單 (以國家/地區為基礎)

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用下列方法來取得特定國家/地區中可用的產品集合。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 國家/地區。

## <a name="c"></a>C\#

若要取得產品清單：

1. 使用您的**iaggregatepartner.customers.byid**集合，透過**ByCountry （）** 方法來選取國家/地區。

2. 使用**ByTargetView （）** 方法選取目錄檢視。

3. 選擇性使用**ByReservationScope （）** 方法選取保留範圍。

4. 選擇性使用**ByTargetSegment （）** 方法選取目標區段。

5. 呼叫**Get （）** 或**GetAsync （）** 方法以傳回集合。

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要取得產品清單：

1. 使用您的**iaggregatepartner.customers.byid. getProducts**函式，透過**byCountry （）** 函數來選取國家/地區。

2. 使用**byTargetView （）** 函數來選取目錄檢視。
3. 選擇性使用**byTargetSegment （）** 函數來選取目標區段。

4. 呼叫**get （）** 函數以傳回集合。

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

若要取得產品清單：

1. 執行[**PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)命令。

2. 藉由指定**目錄**參數來選取目錄。
3. 選擇性藉由指定**區段**參數來選取目標區段。

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products？ country = {country} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

使用下列路徑和查詢參數來取得產品清單。

| 名稱                   | 類型     | 必要 | 描述                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | 字串   | 是      | 國家/地區識別碼。                                                  |
| targetView             | 字串   | 是      | 識別目錄的目標視圖。 支援的值為： <ul><li>**Azure**，其中包括所有 Azure 專案</li><li>**AzureReservations**，其中包括所有的 Azure 保留專案</li><li>**AzureReservationsVM**，其中包括所有虛擬機器（VM）保留專案</li><li>**AzureReservationsSQL**，其中包含所有 SQL 保留專案</li><li>**AzureReservationsCosmosDb**，其中包含所有 Cosmos 資料庫保留專案</li><li>**Microsoftazure.mobileengagement**，其中包含 Microsoft Azure 訂用帳戶（**ms-azr-0017p-流程 ms-azr-0145p**）和 Azure 方案的專案</li><li>**您**，其中包含所有線上服務專案（包括商用 marketplace 產品）</li><li>包含所有軟體專案的**軟體**</li><li>**SoftwareSUSELinux**，其中包含所有軟體 SUSE Linux 專案</li><li>**SoftwarePerpetual**，其中包含所有永久軟體專案</li><li>**SoftwareSubscriptions**，其中包含所有軟體訂閱專案</li></ul> |
| targetSegment          | 字串   | 否       | 識別目標區段。 不同目標物件的視圖。 支援的值為： <ul><li>**商用**</li><li>**教育**</li><li>**身份證**</li><li>**非營利**</li></ul> |
| reservationScope | 字串   | 否 | 查詢 Azure 保留的產品清單時，請指定`reservationScope=AzurePlan`以取得適用于 azure 方案的產品清單。 排除此參數以取得適用于 Microsoft Azure （**ms-azr-0017p-流程 ms-azr-0145p**）訂用帳戶的 Azure 保留產品清單。  |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-examples"></a>要求範例

#### <a name="products-by-country"></a>依國家/地區的產品

遵循此範例以依據國家/地區，取得 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶和 Azure 方案的產品清單。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Azure VM 保留（Azure 方案）

請遵循此範例，依國家/地區為適用于 Azure 方案的 Azure VM 保留專案，取得產品清單。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>適用于 Microsoft Azure 的 Azure VM 保留（MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶

遵循此範例，依據適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的 Azure VM 保留專案，取得各國家/地區的產品清單。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[**產品**](product-resources.md#product)資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼     | 錯誤碼   | 描述                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | 不允許存取要求的 targetSegment。                                                     |
| 403                  | 400036       | 不允許存取要求的 targetView。                                                        |

### <a name="response-example"></a>回應範例

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
