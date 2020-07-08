---
title: 確認合作夥伴的 MPN 識別碼
description: 如何驗證合作夥伴的 Microsoft 合作夥伴網路識別碼（MPN ID）。此處顯示的技術會向合作夥伴中心要求合作夥伴的 MPN 設定檔，以驗證合作夥伴的 Microsoft 合作夥伴網路識別碼。
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5c35cfb024a8894d7f40208f8f93f6f41ee94121
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095210"
---
# <a name="verify-a-partner-mpn-id"></a>確認合作夥伴的 MPN 識別碼

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何驗證合作夥伴的 Microsoft 合作夥伴網路識別碼（MPN ID）。

此處顯示的技術會向合作夥伴中心要求合作夥伴的 MPN 設定檔，以驗證合作夥伴的 Microsoft 合作夥伴網路識別碼。 如果要求成功，則識別碼會視為有效。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

- 要驗證的合作夥伴 MPN 識別碼。 如果您省略此值，要求會抓取已登入夥伴的 MPN 設定檔。

## <a name="c"></a>C\#

若要驗證合作夥伴的 MPN 識別碼，請先從[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)屬性取得夥伴設定檔集合作業的介面。 然後取得介面，以從[**MpnProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile)屬性 MPN 設定檔作業。 最後，使用 MPN 識別碼呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)方法，以取出 MPN 設定檔。 如果您省略 Get 或 GetAsync 呼叫中的 MPN 識別碼，要求會嘗試取出已登入夥伴的 MPN 設定檔。

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： VerifyPartnerMpnId.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/profiles/mpn？ mpnId = {mpn-ID} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

提供下列查詢參數來識別合作夥伴。 如果您省略此查詢參數，要求會傳回已登入夥伴的 MPN 設定檔。

| 名稱   | 類型 | 必要 | 說明                                                 |
|--------|------|----------|-------------------------------------------------------------|
| mpn-id | int  | 否       | 識別合作夥伴的 Microsoft 合作夥伴網路識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含合作夥伴的[MpnProfile](profile-resources.md#mpnprofile)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example-success"></a>回應範例 (成功)

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a>回應範例（失敗）

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
