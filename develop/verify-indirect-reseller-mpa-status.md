---
title: 確認間接轉銷商的 Microsoft 合作夥伴合約簽署狀態
description: 您可以使用 AgreementStatus API 來驗證間接轉銷商是否已簽署 Microsoft 合作夥伴合約。
ms.date: 10/30/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2b7785aa3b419ff5160031fb338e78f7130d5b9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487708"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>確認間接轉銷商的 Microsoft 合作夥伴合約簽署狀態

適用於：

* 合作夥伴中心
* Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用其 Microsoft 合作夥伴網路（MPN）識別碼或雲端解決方案提供者（CSP）租使用者識別碼（Microsoft ID），確認間接轉銷商是否已簽署 Microsoft 合作夥伴合約。 您可以使用其中一個識別碼，以使用**AgreementStatus** API 來檢查 Microsoft 合作夥伴合約簽署狀態。

## <a name="prerequisites"></a>必要條件

* 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例僅支援使用應用程式 + 使用者認證進行驗證。
* 間接轉銷商的 MPN 識別碼或 CSP 租使用者識別碼（Microsoft ID）。 *您必須使用這兩個識別碼的其中一個。*

## <a name="rest"></a>停

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI |
| ------ | ----------- |
| **獲取** | *[{baseURL}](partner-center-rest-urls.md)* /V1/compliance/{ProgramName}/agreementstatus？ mpnId = {mpnId} & tenantId = {tenantId} |

##### <a name="uri-parameters"></a>URI 參數

您必須提供下列兩個查詢參數的其中一個，以識別合作夥伴。 如果您未提供這兩個查詢參數的其中一個，則會收到**400 （不正確的要求）** 錯誤。

| 名稱 | 類型 | 必要 | 描述 |
| ---- | ---- | -------- | ----------- |
| **MpnId** | 整數 | 否 | 識別間接轉銷商的 Microsoft 合作夥伴網路識別碼。 |
| **TenantId** | GUID | 否 | 識別間接轉銷商 CSP 帳戶的 Microsoft 識別碼。 |

#### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](https://docs.microsoft.com/en-us/partner-center/develop/headers)。

#### <a name="request-examples"></a>要求範例

##### <a name="request-using-mpn-id"></a>使用 MPN 識別碼的要求

下列範例要求會使用間接轉銷商的 Microsoft 合作夥伴網路識別碼，取得間接轉銷商的 Microsoft 合作夥伴合約簽署狀態。

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

##### <a name="request-using-csp-tenant-id"></a>使用 CSP 租使用者識別碼的要求

下列範例要求會使用間接轉銷商的 CSP 租使用者識別碼（Microsoft ID），來取得間接轉銷商的 Microsoft 合作夥伴合約簽署狀態。

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="rest-response"></a>REST 回應

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](https://docs.microsoft.com/en-us/partner-center/develop/error-codes)。

#### <a name="response-example-success"></a>回應範例（成功）

下列範例回應會成功傳回間接轉銷商是否已簽署 Microsoft 合作夥伴合約。

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

#### <a name="response-examples-failure"></a>回應範例（失敗）

當間接轉銷商的 Microsoft 合作夥伴合約的簽署狀態無法傳回時，您可能會收到與下列範例類似的回應。

##### <a name="non-guid-formatted-csp-tenant-id"></a>非 GUID 格式的 CSP 租使用者識別碼

當您傳遞至 API 的 CSP 租使用者識別碼不是 GUID 時，會傳回下列範例回應。

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

##### <a name="non-numeric-mpn-id"></a>非數值 MPN 識別碼

當您傳遞至 API 的 MPN 識別碼不是數位時，會傳回下列範例回應。

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

##### <a name="no-mpn-id-or-csp-tenant-id"></a>沒有 MPN 識別碼或 CSP 租使用者識別碼

當您未將 MPN ID 或 CSP 租使用者識別碼傳遞給 API 時，會傳回下列範例回應。 您必須將這兩個識別碼類型的其中一個傳遞給 API。

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

##### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>已傳遞 MPN 識別碼和 CSP 租使用者識別碼

當您將 MPN ID 和 CSP 租使用者識別碼同時傳遞給 API 時，會傳回下列範例回應。 您必須只將這兩個識別碼類型*之一*傳遞給 API。

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```
