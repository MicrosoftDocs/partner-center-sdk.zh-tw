---
title: 取得訂用帳戶的所有每月使用量記錄。
description: 您可以使用 AzureResourceMonthlyUsageRecord 資源集合來取得客戶訂用帳戶內的服務清單，以及其相關聯的分級使用量資訊。
ms.assetid: 037D71B9-8E8B-4BC0-8388-9CBC97218CED
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0acd284c1b829330283d2012fcb6a85d3553f763
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485968"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a>取得訂用帳戶的所有每月使用量記錄。

適用於：

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用[**AzureResourceMonthlyUsageRecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord)資源集合來取得客戶訂用帳戶內的服務清單，以及其相關聯的分級使用量資訊。

## <a name="prerequisites"></a>必要條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（**客戶租使用者 id**）。 如果您沒有客戶的識別碼，您可以從 [customers] 清單中選擇客戶，選取 [**帳戶**]，然後儲存其**Microsoft ID**，以在合作夥伴中心查詢識別碼。
- 訂用帳戶識別碼。

*此 API 僅支援 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶。如果您使用 Azure 方案，請改[為參閱依計量取得訂用帳戶的使用量資料](get-a-customer-subscription-meter-usage-records.md)。*

## <a name="c"></a>C\#

若要取得訂用帳戶的資源使用量資訊：

1. 使用您的**iaggregatepartner.customers.byid. Customers**集合來呼叫**ById （）** 方法。 
2. 呼叫 [訂用帳戶 **] 屬性，以及 [** **usagerecords 和 resources**] 和 [ **Resources** ] 屬性。 
3. 呼叫**Get （）** 或**GetAsync （）** 方法。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

如需範例，請參閱下列各項：

- 範例：[主控台測試應用程式](console-test-app.md)
- 專案： **PartnerSDK. FeatureSample**
- 類別： **SubscriptionResourceUsageRecords.cs**

## <a name="rest"></a>停

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1。1 |

##### <a name="uri-parameters"></a>URI 參數

下表列出所需的查詢參數，以取得評等的使用方式資訊。

| 名稱                    | 類型     | 必要 | 描述                               |
|-------------------------|----------|----------|-------------------------------------------|
| **客戶-租使用者識別碼**  | **guid** | Y        | 對應至客戶的 GUID。     |
| **訂用帳戶識別碼** | **guid** | Y        | 對應至訂用帳戶的 GUID。 |

#### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

#### <a name="request-body"></a>要求本文

無。

#### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**AzureResourceMonthlyUsageRecord**資源的集合。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```