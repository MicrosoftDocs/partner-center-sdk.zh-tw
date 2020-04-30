---
title: 取得客戶的產品升級狀態
description: 您可以使用 ProductUpgradeRequest 資源，將客戶的產品升級狀態判斷為新的產品系列，例如從 Microsoft Azure （MS-MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶到 Azure 方案。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 98737e75c643cb9ca90572544173fe5000f475d9
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157270"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>取得客戶的產品升級狀態

**適用於：**

- 合作夥伴中心

您可以使用[**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest)資源來取得升級到新產品系列的狀態。 當您將客戶從 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶升級為 Azure 方案時，就會套用此資源。 成功的要求會傳回[**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)資源。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。 搭配合作夥伴中心 Api 使用應用程式 + 使用者驗證時，請遵循[安全的應用程式模型](enable-secure-app-model.md)。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 產品系列。

- 升級要求的升級識別碼。

## <a name="c"></a>C\#

若要檢查客戶是否有資格升級至 Azure 方案：

1. 建立**ProductUpgradesRequest**物件，並指定客戶識別碼和 "Azure" 做為產品系列。

2. 使用**iaggregatepartner.customers.byid. ProductUpgrades**集合。

3. 呼叫**ById**方法，並傳入**升級識別碼**。

4. 呼叫**CheckStatus**方法，並傳入**ProductUpgradesRequest**物件，這會傳回**ProductUpgradeStatus**物件。

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

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來指定您要取得產品升級狀態的客戶。

| 名稱               | 類型 | 必要 | 描述                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **升級-識別碼** | GUID | 是 | 值是 GUID 格式的升級識別碼。 您可以使用此識別碼來指定要追蹤的升級。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求主體必須包含[**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest)資源。

### <a name="request-example"></a>要求範例

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

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回主體中的[**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

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
