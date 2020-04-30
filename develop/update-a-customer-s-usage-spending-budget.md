---
title: 更新客戶的使用量支出預算
description: 更新為客戶使用而配置的消費預算。
ms.assetid: D7843FBF-81FC-4FA0-8396-6365E12FB01B
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7afd48db759e776cc832ccba704cf9b188eb8ebb
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157960"
---
# <a name="update-a-customers-usage-spending-budget"></a>更新客戶的使用量支出預算

**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

更新為客戶使用而配置的[消費預算](customer-usage-resources.md#customerusagesummary)。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

## <a name="c"></a>C\#

若要更新客戶的使用量支出預算，請先建立具有更新金額的新[**SpendingBudget**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget)物件。 然後使用[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection)集合，並以指定的客戶識別碼呼叫[**ById （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法。 然後存取[**UsageBudget**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget)屬性，並將更新的使用量預算傳遞至[**Patch （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch)或[**PatchAsync （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync)方法。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **跳** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來更新帳單設定檔。

| 名稱                   | 類型     | 必要 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

完整資源。

### <a name="request-example"></a>要求範例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
     "Amount": 100,
     "Attributes": {
          "ObjectType": "SpendingBudget"
     }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回使用者的支出預算，其中包含更新的金額。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"PATCH",
            "headers":[]
        }
    }
}
```
