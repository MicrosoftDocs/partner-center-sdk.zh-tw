---
title: 檢查客戶是否有資格升級至 Azure 方案
description: 您可以使用 ProductUpgradeRequest 資源來傳回 ProductUpgradesEligibility 資源，以判斷客戶是否有資格從 Microsoft Azure （MS-MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶升級為 Azure 方案。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 71a9cc393b9273a156e0fd3cc434ee668cdaa324
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490298"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>檢查客戶是否有資格升級至 Azure 方案

適用於：

- 合作夥伴中心

您可以使用[**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest)資源來檢查客戶是否有資格從 MICROSOFT AZURE （Ms-azr-0017p-流程 ms-azr-0145p）訂用帳戶升級為 Azure 方案。此方法會傳回具有客戶產品升級資格的[**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)資源。

## <a name="prerequisites"></a>必要條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用應用程式 + 使用者認證進行驗證。 搭配合作夥伴中心 Api 使用應用程式 + 使用者驗證時，請遵循[安全的應用程式模型](enable-secure-app-model.md)。
- 客戶識別碼。
- 產品系列。

## <a name="c"></a>C\#

若要檢查客戶是否有資格升級至 Azure 方案：

1. 建立**ProductUpgradesRequest**物件，並指定客戶識別碼和 "Azure" 做為產品系列。
2. 使用**iaggregatepartner.customers.byid. ProductUpgrades**集合。
3. 呼叫**CheckEligibility**方法，並傳入**ProductUpgradesRequest**物件，這會傳回**ProductUpgradesEligibility**物件。

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest"></a>停

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **發佈** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1。1 |

#### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

#### <a name="request-body"></a>要求本文

要求主體必須包含[**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest)資源。

#### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
