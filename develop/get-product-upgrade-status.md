---
title: 取得客戶的產品升級狀態
description: 您可以使用 ProductUpgradeRequest 資源，將客戶的產品升級狀態判斷為新的產品系列，例如從 Microsoft Azure （MS-MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶到 Azure 方案。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 5ae177c5c57ba12de80884aed3697102a5b1f914
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487288"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>取得客戶的產品升級狀態

適用於：

- 合作夥伴中心

您可以使用[**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest)資源來取得升級到新產品系列的狀態。 當您將客戶從 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶升級為 Azure 方案時，就會套用此資源。 成功的要求會傳回[**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)資源。

## <a name="prerequisites"></a>先決條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用應用程式 + 使用者認證進行驗證。 搭配合作夥伴中心 Api 使用應用程式 + 使用者驗證時，請遵循[安全的應用程式模型](enable-secure-app-model.md)。
- 客戶識別碼。
- 產品系列。
- 升級要求的升級識別碼。

## <a name="c"></a>C\#

若要檢查客戶是否有資格升級至 Azure 方案：

1. 建立**ProductUpgradesRequest**物件，並指定客戶識別碼和 "Azure" 做為產品系列。
2. 使用**iaggregatepartner.customers.byid. ProductUpgrades**集合。
2. 呼叫**ById**方法，並傳入**升級識別碼**。
3. 呼叫**CheckStatus**方法，並傳入**ProductUpgradesRequest**物件，這會傳回**ProductUpgradeStatus**物件。

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```
```

## REST

### REST request

#### Request syntax

| Method   | Request URI |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1 |

#### URI parameter

Use the following query parameter to specify the customer for whom you're getting a product upgrade status.

| Name               | Type | Required | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **upgrade-id** | GUID | Yes | The value is a GUID-formatted upgrade identifier. You can use this identifier to specify an upgrade to track. |

#### Request headers

For more information, see [Partner Center REST headers](headers.md).

#### Request body

The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.

#### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

### <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回主體中的[**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)資源。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
