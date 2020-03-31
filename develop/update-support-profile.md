---
title: 更新支援設定檔
description: 更新使用者的支援設定檔。
ms.assetid: 3F98BD1D-2490-4F0B-A8FF-7D80B7E0690E
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 896665981b001127c6ea1b0c72ea09553eca4ba9
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414656"
---
# <a name="update-support-profile"></a>更新支援設定檔


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

更新使用者的支援設定檔。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要更新您的支援設定檔，請先[取得您的支援設定檔](get-support-profile.md)，並進行任何您想要的變更。 然後，使用您的[**Ipartneroperations.profiles 設定檔**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)集合。 呼叫[**SupportProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile)屬性，後面接著[**Update （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update)或[**UpdateAsync （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync)方法。

``` csharp
// IAggregatePartner partnerOperations;

// updated profile 
SupportProfile newSupportProfile = new SupportProfile
{
   Email = supportProfile.Email,
   Website = supportProfile.Website,
   Telephone = new Random().Next(10000000, 99999999).ToString(CultureInfo.InvariantCulture)
};

SupportProfile updatedSupportProfile = partnerOperations.Profiles.SupportProfile.Update(newSupportProfile);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerCenterSDK. FeaturesSamples**類別**： UpdateSupportProfile.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法  | 要求 URI                                                                     |
|---------|---------------------------------------------------------------------------------|
| **PUT** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1。1 |



**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

完整的支援設定檔資源。

**要求範例**

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/supportprofile HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
Content-Type: application/json
Content-Length: 167
Expect: 100-continue

{
    "Email": "email@sample.com",
    "Telephone": "4255555555",
    "Website": "www.microsoft.com",
    "ProfileType": "support_profile",
    "Attributes": {
        "ObjectType": "PartnerSupportProfile"
    }
}
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，此方法會在回應主體中傳回已更新的**SupportProfile**物件屬性。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
Date: Wed, 25 Nov 2015 07:16:18 GMT

{
    "email": "email@sample.com",
    "telephone": "4255555555",
    "website": "www.microsoft.com",
    "profileType": "support_profile",
    "links": {
        "self": {
            "uri": "/v1/profiles/support",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerSupportProfile"
    }
}
```








