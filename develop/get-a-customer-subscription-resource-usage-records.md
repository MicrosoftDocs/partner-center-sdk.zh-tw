---
title: 依照資源取得訂用帳戶的使用資料
description: 您可以在目前的計費期間，使用 ResourceUsageRecord 資源來取得特定 Azure 服務或資源的客戶資源使用量記錄。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 75e36f0779f7414a03e8de4f5fe0a753a717cacd
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156240"
---
# <a name="get-usage-data-for-subscription-by-resource"></a>依照資源取得訂用帳戶的使用資料

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本文說明如何取得**ResourceUsageRecord**資源。 此資源代表在您的 Azure 方案中布建個別資源的月份匯總總計。 您可以在目前的計費期間，使用此資源來取得特定 Azure 服務或資源的客戶資源使用量記錄。 此 API 會傳回先前無法透過 Azure 消費 Api 使用的資料。

*此路由不支援 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶。*

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 訂用帳戶識別碼

## <a name="c"></a>C\#

若要在目前的計費期間，針對特定的 Azure 服務或資源取得客戶的資源使用量記錄：

1. 使用您的**iaggregatepartner.customers.byid. Customers**集合來呼叫**ById （）** 方法。

2. 呼叫 [訂用帳戶] 屬性，以及 [ **usagerecords 和 resources**] 和 [ **Resources** ] 屬性。 藉由呼叫 Get （）或 GetAsync （）方法來完成。

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

如需範例，請參閱下列各項：

- 範例：[主控台測試應用程式](console-test-app.md)
- 專案： **PartnerSDK. FeatureSamples**
- 類別： **GetSubscriptionUsageRecordsByResource.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1。1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**\<PagedResourceCollection ResourceUsageRecord>** 資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
