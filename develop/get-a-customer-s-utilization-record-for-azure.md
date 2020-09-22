---
title: 取得客戶的 Azure 使用率記錄
description: 您可以使用 Azure 使用率 API，在指定的時段內取得客戶 Azure 訂用帳戶的使用量記錄。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcdeb51b04039fd05b923150c85119385c0537e0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927747"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>取得客戶的 Azure 使用率記錄

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用 Azure 使用率 API，在指定的期間內取得客戶 Azure 訂用帳戶的使用量記錄。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 訂用帳戶識別碼。

此 API 會針對任意時間範圍傳回每日和每小時未分級的耗用量。 不過， *Azure 方案不支援此 API*。 如果您有 Azure 方案，請參閱文章 [取得發票未開立帳單耗用量明細專案](get-invoice-unbilled-consumption-lineitems.md) ，並改為 [取得發票計費的耗用量明細專案](get-invoice-billed-consumption-lineitems.md) 。 這些文章說明如何針對每個資源的每個計量，取得每日層級的分級耗用量。 此速率耗用量相當於 Azure 使用量 API 所提供的每日資料細微性。 您必須使用發票識別碼來取出計費的使用量資料。 或者，您可以使用目前和先前的期間來取得未開立帳單使用量預估。 *Azure 方案訂用帳戶資源目前不支援每小時的資料細微性和任意日期範圍篩選*。

## <a name="azure-utilization-api"></a>Azure 使用量 API

此 Azure 使用量 API 可讓您存取一段時間的使用率記錄，以代表在計費系統中回報使用率的時間。 它可讓您存取用來建立和計算對帳檔案的相同使用率資料。 但是，它並不知道計費系統對帳檔案邏輯。 您不應該預期對帳檔案的摘要結果會比對此 API 所取得的結果，完全符合相同的時間週期。

例如，計費系統會採用相同的使用量資料，並套用延遲規則來判斷對帳檔案中的考慮。 當計費期間結束時，所有使用量會一直到計費期間結束的當天結束為止，並包含在對帳檔案中。 在計費週期結束後24小時內回報的計費期間內，會在下一個對帳檔案中考慮任何延遲的使用量。 如需合作夥伴如何計費的延遲規則，請參閱 [取得 Azure 訂用帳戶的耗用量資料](/previous-versions/azure/reference/mt219001(v=azure.100))。

此 REST API 已分頁。 如果回應承載大於單一頁面，您必須遵循下一個連結來取得下一頁的使用率記錄。

## <a name="c"></a>C\#

若要取得 Azure 使用量記錄：

1. 取得客戶識別碼和訂用帳戶識別碼。

2. 呼叫 [**>iazureutilizationcollection.query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) 方法，以傳回包含使用率記錄的 [**>resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) 。

3. 取得 Azure 使用率記錄列舉值，以跨越使用量頁面。 這是必要步驟，因為已將資源集合分頁。

- **範例**： [主控台測試應用程式](console-test-app.md)
- **專案**：合作夥伴中心 SDK 範例
- **類別**： GetAzureSubscriptionUtilization.cs

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要取得 Azure 使用量記錄，您首先需要客戶識別碼和訂用帳戶識別碼。 然後，您可以呼叫 **>iazureutilizationcollection.query** 函數來傳回包含使用率記錄的 **>resourcecollection** 。 資源集合已分頁，因此您必須取得 Azure 使用率記錄列舉程式才能周遊使用率頁面。

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

若要取得 Azure 使用量記錄，您首先需要客戶識別碼和訂用帳戶識別碼。 然後，您可以呼叫 [**PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md)。 此命令會傳回指定時間內所有可用的記錄。

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI |
|------- | ----------- |
| **GET** | *{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure？開始 \_ 時間 = {開始時間} &結束 \_ 時間 = {結束時間} &資料細微性 = {細微性} &顯示 \_ 詳細資料 = {True} |

#### <a name="uri-parameters"></a>URI 參數

使用下列路徑和查詢參數來取得使用率記錄。

| 名稱 | 類型 | 必要 | 說明 |
| ---- | ---- | -------- | ----------- |
| customer-tenant-id | 字串 | Yes | 用來識別客戶的 GUID 格式字串。 |
| subscription-id | 字串 | Yes | 用來識別訂用帳戶的 GUID 格式字串。 |
| start_time | UTC 日期時間位移格式的字串 | Yes | 時間範圍的開頭，表示計費系統中回報使用率的時間。 |
| end_time | UTC 日期時間位移格式的字串 | Yes | 當計費系統中回報使用率時所代表之時間範圍的結尾。 |
| 資料粒度 | 字串 | No | 定義使用量彙總的細微性。 可用的選項包括： `daily` (預設) 和 `hourly` 。
| show_details | boolean | No | 指定是否要取得執行個體層級的使用量詳細資料。 預設值為 `true`。 |
| 大小 | number | No | 指定單一 API 呼叫所傳回的彙總數目。 預設值是 1000。 最大值為1000。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無

### <a name="request-example"></a>要求範例

下列範例要求會產生類似于期間 7/2-8/1 的對帳檔案所顯示的結果。 這些結果可能不完全相符 (請參閱 [Azure 使用量 API](#azure-utilization-api) ，以取得詳細資料) 一節。

此範例要求會傳回在7/2 （上午12點）上午12點（上午12點）之間的計費系統中回報的使用量資料 (UTC) 和 8/2 (上午12： UTC) 。

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回 [Azure 使用率記錄](azure-utilization-record-resources.md) 資源的集合。 如果相依系統中的 Azure 使用量資料尚未就緒，這個方法會傳回 HTTP 狀態碼204，並包含重試標頭。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 使用網路追蹤工具來讀取 HTTP 狀態碼、 [錯誤碼類型](error-codes.md)和其他參數。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
