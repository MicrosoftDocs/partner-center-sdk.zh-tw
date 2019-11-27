---
title: 取得客戶訂用帳戶的使用量摘要
description: 您可以使用 SubscriptionUsageSummary 資源，在目前的計費期間取得特定 Azure 服務或資源的訂用帳戶使用量摘要。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: c2890b1fc57686c08bf7fe0e0dfed0c50dc880b6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487668"
---
# <a name="get-usage-summary-for-customers-subscription"></a>取得客戶訂用帳戶的使用量摘要

適用於：

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用**SubscriptionUsageSummary**資源來取得客戶的訂用帳戶使用量摘要。 此資源代表在目前計費期間內特定 Azure 服務或資源的訂用帳戶使用方式摘要。

## <a name="prerequisites"></a>必要條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例僅支援使用應用程式 + 使用者認證進行驗證。
- 客戶識別碼（**客戶租使用者 id**）。 如果您沒有客戶的識別碼，您可以從 [customers] 清單中選擇客戶，選取 [**帳戶**]，然後儲存其**Microsoft ID**，以在合作夥伴中心查詢識別碼。
- 訂用帳戶識別碼

## <a name="c"></a>C\#

若要取得客戶訂用帳戶的訂用帳戶使用摘要：

1. 使用您的**iaggregatepartner.customers.byid. Customers**集合來呼叫**ById （）** 方法。
2. 然後呼叫 [訂用帳戶] 屬性，以及 [ **UsageSummary** ] 屬性。 藉由呼叫 Get （）或 GetAsync （）方法來完成。

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

如需範例，請參閱下列各項：

- 範例：[主控台測試應用程式](console-test-app.md)
- 專案： **PartnerSDK. FeatureSamples**
- 類別： **GetSubscriptionUsageSummary.cs**

## <a name="rest"></a>停

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1。1 |

##### <a name="uri-parameters"></a>URI 參數

下表列出所需的查詢參數，以取得客戶的評等使用量資訊。

| 名稱                   | 類型     | 必要 | 描述                               |
|------------------------|----------|----------|-------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 對應至客戶的 GUID。     |
| **訂用帳戶識別碼**    | **guid** | Y        | 對應至訂用帳戶識別碼的 GUID。 若為 Azure 方案，這是對應合作夥伴中心訂用帳戶[資源](subscription-resources.md#subscription)的識別碼，代表 Azure 方案。 *針對 Azure 方案訂用帳戶資源，請提供**方案識別碼**作為此路由中的訂用帳戶**識別碼**。* |

#### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

無。

#### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**SubscriptionUsageSummary**資源。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

#### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱的回應範例

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
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a>Azure 方案的回應範例

在此範例中，客戶購買了 Azure 方案。

*針對具有 Azure 方案的客戶，會有下列 API 回應變更：*

- **currencyLocale**已取代為**currencyCode**
- **usdTotalCost**是新的欄位

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
