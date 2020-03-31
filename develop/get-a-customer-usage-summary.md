---
title: 取得所有客戶訂用帳戶的使用量摘要
description: 您可以在目前的計費期間，使用 Customerrelationshiprequest 資源來取得客戶特定 Azure 服務或資源的使用方式。
ms.assetid: 58FA3CBD-27CF-46C5-9EB2-188D83896F7D
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: afa4b40d18b104270ea047eab383a917d6bc7a0a
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415673"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a>取得所有客戶訂用帳戶的使用量摘要

適用於：

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以在目前的計費期間，使用**customerrelationshiprequest**資源來取得客戶特定 Azure 服務或資源的使用方式。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼 (**customer-tenant-id**)。 如果您沒有客戶的識別碼，您可以從 [customers] 清單中選擇客戶，選取 [**帳戶**]，然後儲存其**Microsoft ID**，以在合作夥伴中心查詢識別碼。

## <a name="c"></a>C\#

若要取得所有客戶訂用帳戶的使用摘要：

1. 使用您的**iaggregatepartner.customers.byid. Customers**集合來呼叫**ById （）** 方法。
2. 呼叫**UsageSummary**屬性，後面接著**Get （）** 或**GetAsync （）** 方法：

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

如需範例，請參閱下列各項：

- 範例：[主控台測試應用程式](console-test-app.md)
- 專案： **PartnerSDK. FeatureSamples**
- 類別： **GetCustomerUsageSummary.cs**

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1。1 |

##### <a name="uri-parameter"></a>URI 參數

下表列出必要的查詢參數，以取得客戶的評等使用量資訊。

| 名稱                   | 類型     | 必要項 | 描述                           |
|------------------------|----------|----------|---------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 對應至客戶的 GUID。 |

#### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

None。

#### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**customerrelationshiprequest**資源。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

#### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a>Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的回應範例

在此範例中，客戶購買了**145P Azure PayG**供應專案。

*對於具有 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的客戶，API 回應不會有任何變更。*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

#### <a name="response-example-for-azure-plan"></a>Azure 方案的回應範例

在此範例中，客戶購買了 Azure 方案。

*針對具有 Azure 方案的客戶，API 回應有下列變更：*

- **currencyLocale**已取代為**currencyCode**
- **usdTotalCost**是新的欄位

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
