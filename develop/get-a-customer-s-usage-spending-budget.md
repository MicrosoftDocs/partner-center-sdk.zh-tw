---
title: 取得客戶的使用量支出預算
description: 您可以使用支出預算（SpendingBudget 物件）來更新客戶使用量摘要（Customerrelationshiprequest 資源）。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dd402187e5f41bcc6b6abd47c93553f2c8d2e865
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414121"
---
# <a name="get-a-customers-usage-spending-budget"></a>取得客戶的使用量支出預算

適用於：

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以在[客戶使用量摘要（ **customerrelationshiprequest**資源）](customer-usage-resources.md#customerusagesummary)中更新支出預算（ **SpendingBudget**物件）。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼 (**customer-tenant-id**)。 如果您沒有客戶的識別碼，您可以從 [customers] 清單中選擇客戶，選取 [**帳戶**]，然後儲存其**Microsoft ID**，以在合作夥伴中心查詢識別碼。

## <a name="c"></a>C\#

若要更新客戶的使用量支出預算：

1. 建立具有更新金額的新[**SpendingBudget**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget)物件。
2. 使用[**iaggregatepartner.customers.byid. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection)集合，以指定的客戶識別碼呼叫[**ById （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法。
3. 呼叫[**get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync)方法，以取得客戶的使用量預算。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{  
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget HTTP/1。1 |

##### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來更新帳單設定檔。

| 名稱                   | 類型     | 必要項 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。 |

#### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

完整資源。

#### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

### <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回使用者的支出預算，其中包含更新的金額。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

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
            "method":"GET",
            "headers":[]
        }
    }
}
```
