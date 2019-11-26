---
title: Get licenses assigned to a user
description: Get a list of licenses assigned to a user within a customer account.
ms.assetid: 87DC74A1-92E2-4639-BC4C-168A677F5F52
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 73997593b0997a0faca8d702b527e57266a45dfb
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488958"
---
# <a name="get-licenses-assigned-to-a-user"></a>Get licenses assigned to a user

適用於：

- 合作夥伴中心

How to get a list of licenses assigned to a user within a customer account. The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory. To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).

## <a name="prerequisites"></a>必要條件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A customer identifier.
- A user identifier.

## <a name="c"></a>C#

To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer. Then call the [**Users.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user. Next, get an interface to customer user license operations from the [**Licenses**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property. Finally, call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1 |

### <a name="uri-parameter"></a>URI 參數

Use the following path parameters to identify the customer and user.

| 名稱        | 在工作列搜尋方塊中輸入   | 必要 | 說明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | 字串 | [是]      | A GUID formatted string that identifies the customer. |
| user-id     | 字串 | [是]      | A GUID formatted string that identifies the user.     |

### <a name="request-headers"></a>要求標頭

See [Partner Center REST headers](headers.md) for more information.

### <a name="request-body"></a>要求主體

無。

### <a name="request-example"></a>要求的範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST response

If successful, the response body contains the collection of [License](license-resources.md#license) resources.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 3883
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CV: WYkHYMfWTUajFosK.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 00:29:24 GMT

{
    "totalCount": 1,
    "items": [{
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```