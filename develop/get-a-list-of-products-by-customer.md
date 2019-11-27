---
title: 取得產品清單（依客戶）
description: 您可以使用客戶識別碼來取得依客戶的產品集合。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ac244c6b6d561d93be47e232c5b3e4fdbc440707
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487328"
---
# <a name="get-a-list-of-products-by-customer"></a>取得產品清單（依客戶）

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用下列方法來取得現有客戶的產品集合。

## <a name="prerequisites"></a>先決條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（**客戶租使用者 id**）。

## <a name="rest"></a>停

### <a name="rest-request"></a>Rest 要求

#### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/V1/customers/{customer-tenant-id}/products？ targetView = {TARGETVIEW} HTTP/1。1 |

#### <a name="request-uri-parameters"></a>要求 URI 參數

| 名字               | 類型 | 必要 | 說明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | GUID | 是 | 值是 GUID 格式的**客戶租使用者**識別碼，這是可讓您指定客戶的識別碼。 |
| **targetView** | string | 是 | 識別目錄的目標視圖。 支援的值為： <ul><li>**Azure**，其中包括所有 Azure 專案</li><li>**AzureReservations**，其中包括所有的 Azure 保留專案</li><li>**AzureReservationsVM**，其中包括所有虛擬機器（VM）保留專案</li><li>**AzureReservationsSQL**，其中包含所有 SQL 保留專案</li><li>**AzureReservationsCosmosDb**，其中包含所有 Cosmos 資料庫保留專案</li><li>**Microsoftazure.mobileengagement**，其中包含 Microsoft Azure 訂用帳戶（**ms-azr-0017p-流程 ms-azr-0145p**）和 Azure 方案的專案</li><li>**您**，其中包含所有線上服務專案，包括商用 marketplace 產品</li><li>包含所有軟體專案的**軟體**</li><li>**SoftwareSUSELinux**，其中包含所有軟體 SUSE Linux 專案</li><li>**SoftwarePerpetual**，其中包含所有永久軟體專案</li><li>**SoftwareSubscriptions**，其中包含所有軟體訂閱專案 </ul> |

#### <a name="request-header"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

無。

#### <a name="request-example"></a>要求的範例

要求提供給特定客戶的 Azure 使用量型產品清單。 針對公用雲端中的客戶，將會傳回 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）和 Azure 方案的產品：

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

### <a name="rest-response"></a>Rest 回應

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

這個方法會傳回下列錯誤碼：

| HTTP 狀態碼 | 錯誤碼   | 說明                     |
|------------------|--------------|---------------------------------|
| 403 | 400036 | 不允許存取要求的 targetView。 | 

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
 
{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```