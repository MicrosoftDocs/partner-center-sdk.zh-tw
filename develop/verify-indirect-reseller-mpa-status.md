---
title: 確認間接轉銷商的 Microsoft 合作夥伴合約簽署狀態
description: 您可以使用 AgreementStatus API 來確認間接轉銷商是否已簽署 Microsoft 合作夥伴合約。
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4836a5e0646e1f00807966d3d8d332c026276c61
ms.sourcegitcommit: 68a5497a7350e135358aeb7f2a54c75707f922c5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87261937"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>確認間接轉銷商的 Microsoft 合作夥伴合約簽署狀態

**適用於：**

- 合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用 Microsoft 合作夥伴網路 (MPN) 識別碼或雲端解決方案提供者 (CSP) 租用戶識別碼 (Microsoft 識別碼)，確認間接轉銷商是否已簽署 Microsoft 合作夥伴合約。 您可以使用其中一個識別碼，透過 **AgreementStatus** API 來查看 Microsoft 合作夥伴合約簽署狀態。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

- 間接轉銷商的 MPN 識別碼或 CSP 租用戶識別碼 (Microsoft 識別碼)。 您必須使用這兩個識別碼的其中一個。

## <a name="c"></a>C\#

若要取得間接轉銷商的 Microsoft 合作夥伴合約簽署狀態：

1. 使用您的 **IAggregatePartner.Compliance** 集合呼叫 **AgreementSignatureStatus** 屬性。

2. 呼叫 [**Get()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) 或 [**GetAsync()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) 方法。

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- 範例： **[主控台測試應用程式](console-test-app.md)**
- 專案：**PartnerCenterSDK.FeaturesSamples**
- 類別：**GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI |
| ------ | ----------- |
| **GET** | *[{baseURL}](partner-center-rest-urls.md)* /v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

#### <a name="uri-parameters"></a>URI 參數

您必須提供下列兩個查詢參數的其中一個，才能識別合作夥伴。 如果您未提供這兩個查詢參數的其中一個，則會收到 **400 (不正確的要求)** 錯誤。

| 名稱 | 類型 | 必要 | 說明 |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | 否 | 識別間接轉銷商的 Microsoft 合作夥伴網路識別碼。 |
| **TenantId** | GUID | 否 | 識別間接轉銷商 CSP 帳戶的 Microsoft 識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](https://docs.microsoft.com/partner-center/develop/headers)。

### <a name="request-examples"></a>要求範例

#### <a name="request-using-mpn-id"></a>使用 MPN 識別碼的要求

下列要求範例會使用間接轉銷商的 Microsoft 合作夥伴網路識別碼，取得間接轉銷商的 Microsoft 合作夥伴合約簽署狀態。

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>使用 CSP 租用戶識別碼的要求

下列要求範例會使用間接轉銷商的 CSP 租用戶識別碼 (Microsoft 識別碼)，取得間接轉銷商的 Microsoft 合作夥伴合約簽署狀態。

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](https://docs.microsoft.com/partner-center/develop/error-codes)。

### <a name="response-example-success"></a>回應範例 (成功)

下列回應範例會成功傳回間接轉銷商是否已簽署 Microsoft 合作夥伴合約。

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

### <a name="response-examples-failure"></a>回應範例 (失敗)

當間接轉銷商的 Microsoft 合作夥伴合約簽署狀態無法傳回時，您可能會收到與下列範例類似的回應。

#### <a name="non-guid-formatted-csp-tenant-id"></a>非 GUID 格式的 CSP 租用戶識別碼

當您傳遞至 API 的 CSP 租用戶識別碼不是 GUID 時，會傳回下列回應範例。

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

#### <a name="non-numeric-mpn-id"></a>非數值的 MPN 識別碼

當您傳遞至 API 的 MPN 識別碼不是數值時，會傳回下列回應範例。

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a>沒有 MPN 識別碼或 CSP 租用戶識別碼

當您未將 MPN 識別碼或 CSP 租用戶識別碼傳遞給 API 時，會傳回下列回應範例。 您必須將這兩個識別碼類型的其中一個傳遞給 API。

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>同時傳遞 MPN 識別碼和 CSP 租用戶識別碼

當您將 MPN 識別碼和 CSP 租用戶識別碼同時傳遞給 API 時，會傳回下列回應範例。 您只能將兩個識別碼類型的「其中一個」  傳遞給 API。

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

#### <a name="csp-indirect-reseller-mpn-id-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>CSP 間接轉銷商 MPN 識別碼無效，或未從 Partner Membership Center 遷移至合作夥伴中心

當傳遞的間接轉銷商 MPN 識別碼無效或未從 Partner Membership Center 遷移至合作夥伴中心時，會傳回下列範例回應。 [深入了解](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>CSP 間接提供者區域和 CSP 間接轉銷商區域不符

當間接轉銷商 MPN 識別碼的區域與間接提供者的區域不符時，會傳回下列範例回應。 [深入了解](https://docs.microsoft.com/partner-center/regional-authorization-overview) CSP 區域。

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
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/en-us/partner-center/regional-authorization-overview" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>CSP 間接轉銷商帳戶存在於合作夥伴中心，但尚未簽署 MPA

當合作夥伴中心內的 CSP 間接轉銷商帳戶尚未簽署 MPA 時，會傳回下列範例回應。 [深入了解](https://partner.microsoft.com/resources/detail/verify-mpa-acceptance-status-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://partner.microsoft.com/en-gb/resources/detail/verify-mpa-acceptance-status-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>沒有任何 CSP 間接轉銷商帳戶與指定的 MPN 識別碼相關聯

當合作夥伴中心可以辨識要求中所傳遞的 MPN 識別碼，但沒有任何 CSP 註冊與指定的 MPN 識別碼相關聯時，就會傳回下列範例回應。 [深入了解](https://partner.microsoft.com/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a>無效的租用戶識別碼

當合作夥伴中心找不到任何與要求中傳遞的租用戶識別碼相關聯的帳戶時，就會傳回下列範例回應。

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>找不到具有指定租用戶識別碼的 MPA

當合作夥伴中心找不到任何具有指定租用戶識別碼的 MPA 簽章時，就會傳回下列範例回應。

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [],
    "source": "PartnerFD"
}
```
