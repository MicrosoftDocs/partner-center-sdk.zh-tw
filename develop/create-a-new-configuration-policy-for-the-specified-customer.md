---
title: Create a new configuration policy for the specified customer
description: How to create a new configuration policy for the specified customer.
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
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a>Create a new configuration policy for the specified customer

適用於：

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

How to create a new configuration policy for the specified customer.

## <a name="prerequisites"></a>必要條件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- The customer identifier.

## <a name="c"></a>C\#

To create a new configuration policy for the specified customer:

1. Instantiate a new [**ConfigurationPolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet. Then call the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.
2. Retrieve the [**ConfigurationPolicies**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.
3. Call the [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.

### <a name="c-example"></a>C\# example

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

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                              |
|----------|------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1 |

#### <a name="uri-parameter"></a>URI 參數

Use the following path parameters when creating the request.

| 名稱        | 在工作列搜尋方塊中輸入   | 必要 | 說明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | 字串 | [是]      | A GUID-formatted string that identifies the customer. |

### <a name="request-headers"></a>要求標頭

See [Partner Center REST headers](headers.md) for more information.

### <a name="request-body"></a>要求主體

The request body must contain an object with the configuration policy information as described in the following table:

| 名稱           | 在工作列搜尋方塊中輸入             | 必要 | 說明                      |
|----------------|------------------|----------|----------------------------------|
| name           | 字串           | [是]      | The friendly name of the policy. |
| 類別       | 字串           | [是]      | The policy category.             |
| 描述    | 字串           | 無       | The policy description.          |
| policySettings | array of strings | [是]      | The policy settings.             |

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

## <a name="rest-response"></a>REST response

If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

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