---
title: 為指定的客戶建立新的設定原則
description: 如何為指定的客戶建立新的設定原則。
ms.assetid: 95649991-A950-4F43-87E8-3EB1E7D06FCD
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0ad89c0fe5e6b3c182315bf5343d78941f7cdd2d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489498"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a>為指定的客戶建立新的設定原則

適用於：

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何為指定的客戶建立新的設定原則。

## <a name="prerequisites"></a>先決條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼。

## <a name="c"></a>C\#

為指定的客戶建立新的設定原則：

1. 將新的[**ConfigurationPolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy)物件具現化，如下列程式碼片段所示。 然後使用客戶識別碼呼叫[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，以在指定的客戶上取得作業的介面。
2. 取出[**ConfigurationPolicies**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies)屬性，以取得設定原則集合作業的介面。
3. 呼叫[**create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)方法來建立設定原則。

### <a name="c-example"></a>C\# 範例

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： CreateConfigurationPolicy.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                              |
|----------|------------------------------------------------------------------------------------------|
| **發佈** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

建立要求時，請使用下列路徑參數。

| 名字        | 類型   | 必要 | 說明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 客戶識別碼 | string | 是      | 識別客戶的 GUID 格式字串。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求主體必須包含具有設定原則資訊的物件，如下表所述：

| 名字           | 類型             | 必要 | 說明                      |
|----------------|------------------|----------|----------------------------------|
| name           | string           | 是      | 原則的易記名稱。 |
| category       | string           | 是      | 原則類別目錄。             |
| 描述    | string           | 否       | 原則描述。          |
| policySettings | 字串陣列 | 是      | 原則設定。             |

### <a name="request-example"></a>要求的範例

```http
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含新原則的[ConfigurationPolicy](device-deployment-resources.md#configurationpolicy)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```