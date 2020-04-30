---
title: 取得 Microsoft 合作夥伴網路設定檔
description: 取得物件，代表合作夥伴的 MPN 設定檔。
ms.assetid: 6DC85E2F-0AC8-4166-883B-CCFD19044FC1
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b8b4d757bb881cac5f261e15f34eb49822f3af30
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157300"
---
# <a name="get-microsoft-partner-network-profile"></a>取得 Microsoft 合作夥伴網路設定檔

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得物件，代表合作夥伴的 MPN 設定檔。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

## <a name="c"></a>C\#

若要取得合作夥伴網路設定檔，請使用**iaggregatepartner.customers.byid 的配置**檔集合，並呼叫**MpnProfile**屬性。 最後，呼叫[**Get （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get)或[**GetAsync （）**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)方法。

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**:P Artnercentersdk. FeaturesSamples**類別**： GetMPNProfile.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要取得合作夥伴網路設定檔，請使用您的**iaggregatepartner.customers.byid. ipartner.getprofiles**函數，並呼叫**getMpnProfile**函式。 最後，呼叫**get （）** 函數。

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

若要取得合作夥伴網路設定檔，請執行[**PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md)命令。

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                          |
|---------|----------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**MPNProfile**物件。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
Date: Mon, 21 Mar 2016 05:51:29 GMT

{
    "mpnId":"<mpnID>",
    "profileType":"MpnProfile",
    "links":{
        "self":{
            "uri":"/profiles/mpn",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"MpnProfile"
    }
}
```
