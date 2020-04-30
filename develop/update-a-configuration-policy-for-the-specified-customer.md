---
title: 為指定客戶更新設定原則
description: 如何為指定的客戶更新指定的設定原則。
ms.assetid: E2B91AC4-B8E8-4A77-AFB7-0CCEF5136621
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 93e876d17eabf458ae0cd1c73fa02c5f634296e3
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157630"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>為指定客戶更新設定原則

**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何為指定的客戶更新指定的設定原則。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 原則識別碼。

## <a name="c"></a>C\#

若要更新指定之客戶的現有設定原則，請將新的[**ConfigurationPolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy)物件具現化，如下列程式碼片段所示。 這個新物件中的值會取代現有物件中的對應值。 然後，使用客戶識別碼呼叫[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，以在指定的客戶上取得作業的介面。 接下來，使用原則識別碼呼叫[**ConfigurationPolicies. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid)方法，以取得指定原則之設定原則作業的介面。 最後，呼叫[**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch)或[**PatchAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync)方法來更新設定原則。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： UpdateConfigurationPolicy.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **提出** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

建立要求時，請使用下列路徑參數。

| 名稱        | 類型   | 必要 | 描述                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| customer-id | 字串 | 是      | 用來識別客戶的 GUID 格式字串。         |
| 原則-識別碼   | 字串 | 是      | GUID 格式的字串，用來識別要更新的原則。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求主體必須包含提供原則資訊的物件。

| 名稱            | 類型             | 必要 | 可更新 | 描述                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| id              | 字串           | 是      | 否        | 可識別原則的 GUID 格式字串。                                                                                                    |
| NAME            | 字串           | 是      | 是       | 原則的易記名稱。                                                                                                                         |
| category        | 字串           | 是      | 否        | 原則類別目錄。                                                                                                                                     |
| description     | 字串           | 否       | 是       | 原則描述。                                                                                                                                  |
| devicesAssigned | number           | 否       | 否        | 裝置數目。                                                                                                                                   |
| policySettings  | 字串的陣列 | 是      | 是       | 原則設定： [無]、[移除\_oem\_預先安裝]、[oobe\_使用者\_不\_是本機\_系統管理員]、[\_略\_過快速設定]、 \_[\_略過 oem 註冊\_]、[略過 eula]。 |

### <a name="request-example"></a>要求範例

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含新原則的[ConfigurationPolicy](device-deployment-resources.md#configurationpolicy)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
