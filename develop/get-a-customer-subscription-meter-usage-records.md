---
title: 依照計量取得訂用帳戶的使用資料
description: 您可以使用 MeterUsageRecord 資源集合，在目前的計費期間取得特定 Azure 服務或資源的客戶計量使用量記錄。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9a84255f479b2faf1954cadabcf6f71274a5f053
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154330"
---
# <a name="get-usage-data-for-subscription-by-meter"></a>依照計量取得訂用帳戶的使用資料

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用**MeterUsageRecord**資源集合，在目前的計費期間取得特定 Azure 服務或資源的客戶計量使用量記錄。 此資源集合代表整個 Azure 方案中目前計費週期的每個計量匯總總計。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 訂用帳戶識別碼

*這個新的路由相當於`subscriptions/{subscription-id}/usagerecords/resources`，它只會繼續針對 MICROSOFT AZURE （Ms-azr-0017p-流程 ms-azr-0145p）訂用帳戶運作。* 這個新的路由將同時支援 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶和 Azure 方案。 若要取得 Azure 方案的這項資訊，您必須切換到這個新的路由。 除了下列各節所述的屬性以外，回應與舊的路由相同。

## <a name="c"></a>C\#

在目前計費期間，針對特定 Azure 服務或資源取得客戶的計量使用量記錄：

1. 使用您的**iaggregatepartner.customers.byid. Customers**集合來呼叫**ById （）** 方法。

2. 呼叫 [訂用帳戶] 屬性，然後**usagerecords 和 resources**[**計量**] 屬性。 藉由呼叫 Get （）或 GetAsync （）方法來完成。

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

如需範例，請參閱下列範例：

- 範例：[主控台測試應用程式](console-test-app.md)
- 專案： **PartnerSDK. FeatureSamples**
- 類別： **GetSubscriptionUsageRecordsByMeter.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

下表列出所需的查詢參數，以取得客戶的評等使用量資訊。

| 名稱                   | 類型     | 必要 | 描述                               |
|------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 對應至客戶的 GUID。     |
| **訂用帳戶識別碼**    | **guid** | Y        | 對應至合作夥伴中心訂用帳戶[資源](subscription-resources.md#subscription)識別碼的 GUID，代表 MICROSOFT AZURE （Ms-azr-0017p-流程 ms-azr-0145p）訂用帳戶或 Azure 方案。 *針對 Azure 方案訂用帳戶資源，請提供**方案識別碼**作為此路由中的訂用帳戶**識別碼**。* |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**\<PagedResourceCollection MeterUsageRecord>** 資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱的回應範例

在此範例中，客戶已購買**145P Azure PayG**。

*對於具有 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的客戶，API 回應不會有任何變更。*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Azure 方案的 REST 回應範例

在此範例中，客戶購買了 Azure 方案。

*針對具有 Azure 方案的客戶，API 回應中有下列變更：*

- **currencyLocale**已取代為**currencyCode**
- **usdTotalCost**是新的欄位

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
