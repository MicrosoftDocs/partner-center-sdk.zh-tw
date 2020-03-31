---
title: 取得依授權群組指派給使用者的授權
description: 如何取得指定授權群組的使用者指派授權清單。
ms.assetid: 8BC0B0BA-894D-42F8-8186-6963AA02E9F6
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6eb55645c6d3ef2663799a4966e9993280fbfc35
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415820"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a>取得依授權群組指派給使用者的授權

**適用於**

- 夥伴中心

如何取得指定授權群組的使用者指派授權清單。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼。
- 使用者識別碼。
- 一或多個授權群組識別碼的清單。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要從指定的授權群組中檢查指派給使用者的授權，請從具現化[**LicenseGroupId**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)類型的[清單](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)開始，然後將授權群組新增至清單。 然後，使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法搭配客戶識別碼來識別客戶。 接下來，使用使用者識別碼呼叫[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法，以識別使用者。 然後，從 [[**授權**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses)] 屬性取得客戶使用者授權作業的介面。 最後，將授權群組清單傳遞給[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync)方法，以取得指派給使用者的授權集合。

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求

**要求語法**

| 方法  | 要求 URI                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/V1/customers/{customer-id}/users/{user-id}/licenses？ LicenseGroupIds = Group1 HTTP/1。1                        |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/V1/customers/{customer-id}/users/{user-id}/licenses？ LicenseGroupIds = Group2 HTTP/1。1                        |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/V1/customers/{customer-id}/users/{user-id}/licenses？ LicenseGroupIds = Group1 & LicenseGroupIds = Group2 HTTP/1。1 |


**URI 參數**

使用下列路徑和查詢參數來識別客戶、使用者和授權群組。

| 名稱            | 類型   | 必要項 | 描述                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 客戶識別碼     | string | 是      | 識別客戶的 GUID 格式字串。                                                                                                                                                                                                                 |
| user-id         | string | 是      | 識別使用者的 GUID 格式字串。                                                                                                                                                                                                                     |
| licenseGroupIds | string | 否       | 列舉值，表示所指派授權的授權群組。 有效值： Group1、Group2 Group1-此群組具有可在 Azure Active Directory （AAD）中管理其授權的所有產品。 Group2-此群組只有 Minecraft 產品授權。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 回應

如果成功，回應主體會包含[授權](license-resources.md#license)資源的集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
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

**回應範例（找不到相符的授權）**

如果找不到指定之授權群組的相符授權，回應會包含空集合，其值為0的 totalCount 元素。

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```