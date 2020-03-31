---
title: 取得組織設定檔
description: 取得物件，代表合作夥伴的組織設定檔。
ms.assetid: 2AA159F1-CC84-4367-A2AF-DFA4C8B0E673
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c4b75b001afbc6e9c7e9c772e9c3f43d85e1dbd8
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416015"
---
# <a name="get-an-organization-profile"></a>取得組織設定檔

**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得物件，代表合作夥伴的組織設定檔。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>範例

### <a name="c"></a>C#

若要取得您的組織設定檔，請使用您的**Iaggregatepartner.customers.byid 配置**檔集合，並呼叫**OrganizationProfile**屬性。 最後，呼叫[**Get （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get)或[**GetAsync （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync)方法。

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerCenterSDK. FeaturesSamples**類別**： GetOrganizationProfile.cs

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

若要取得您的組織設定檔，請使用您的**iaggregatepartner.customers.byid. ipartner.getprofiles**函數，並呼叫**getOrganizationProfile**函式。 最後，呼叫**get （）** 函數。

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

若要取得您的組織設定檔，請執行[**PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md)命令。 

```powershell
Get-PartnerOrganizationProfile
```

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求

**要求語法**

| 方法  | 要求 URI                                                                   |
|---------|-------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1。1 |

**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應

如果成功，此方法會在回應主體中傳回**OrganizationProfile**物件。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
Date: Tue, 22 Mar 2016 17:11:06 GMT

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "profileType":"OrganizationProfile",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```