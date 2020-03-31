---
title: 為客戶新增已驗證的網域
description: 將已驗證的網域新增至合作夥伴中心內的客戶已核准的網域清單。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 89ff3dd9ad8d752f559f23a886d632f60b846eac
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412596"
---
# <a name="add-a-verified-domain-for-a-customer"></a>為客戶新增已驗證的網域

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何將已驗證的網域新增至現有客戶的核准網域清單。

## <a name="prerequisites"></a>必要條件

- 您必須是網域註冊機構的夥伴。
- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（**CustomerTenantId**）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [**帳戶**]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。

## <a name="adding-a-verified-domain"></a>新增已驗證的網域

如果您是身為網域註冊機構的合作夥伴，您可以使用 verifieddomain API 將新的[網域](#domain)資源張貼到現有客戶的網域清單。 若要這麼做，請使用使用者的 CustomerTenantId 來識別客戶、指定 VerifiedDomainName 屬性的值，然後在要求中傳遞包含必要名稱、功能、AuthenticationType、狀態和 VerificationMethod 屬性的[網域](#domain)資源。 若要指定新的[網域](#domain)是同盟網域，請將[網域](#domain)資源中的 AuthenticationType 屬性設定為「同盟」，並在要求中包含[DomainFederationSettings](#domain-federation-settings)資源。 如果方法成功，回應將會包含新的已驗證網域的[網域](#domain)資源。

### <a name="custom-verified-domains"></a>自訂驗證的網域

新增自訂的已驗證網域時，未在**onmicrosoft.com**上註冊的網域，您必須將[CustomerUser. immutableId](user-resources.md#customeruser)屬性設定為您要為其新增網域之客戶的唯一識別碼值。 在驗證過程中，當網域正在進行驗證時，就需要這個唯一的識別碼。 如需客戶使用者帳戶的詳細資訊，請參閱為[客戶建立使用者帳戶](create-user-accounts-for-a-customer.md)。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來指定您要為其新增已驗證網域的客戶。

| 名稱                   | 類型     | 必要項 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | 此值是 GUID 格式的**CustomerTenantId** ，可讓您指定客戶。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的必要屬性。

| 名稱                                                  | 類型   | 必要項                                      | 描述                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | string | 是                                           | 已驗證的功能變數名稱。 |
| [網域](#domain)                                     | object | 是                                           | 包含網域資訊。 |
| [DomainFederationSettings](#domain-federation-settings) | object | 是（如果 AuthenticationType = "同盟"）     | 網域同盟設定，以在網域是「同盟」網域而非「受控」網域時使用。 |

#### <a name="domain"></a>網域

下表描述要求主體中的必要和選擇性**網域**屬性。

| 名稱               | 類型                                     | 必要項 | 描述                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | string           | 是      | 定義網域是否為「受控」網域或「同盟」網域。 支援的值： Managed、同盟。|
| 功能                                            | string           | 是      | 指定網域功能。 例如，"Email"。                  |
| IsDefault                                             | 可為 null 的布林值 | 否       | 指出網域是否為租使用者的預設網域。 支援的值： True、False、Null。        |
| IsInitial                                             | 可為 null 的布林值 | 否       | 指出網域是否為初始網域。 支援的值： True、False、Null。                       |
| 名稱                                                  | string           | 是      | 網域名稱。                                                          |
| RootDomain                                            | string           | 否       | 根域的名稱。                                              |
| 狀態                                                | string           | 是      | 網域狀態。 例如，「已驗證」。 支援的值：未驗證、已驗證、PendingDeletion。                               |
| VerificationMethod                                    | string           | 是      | 網域驗證方法類型。 支援的值： None、DnsRecord、Email。                                    |

##### <a name="domain-federation-settings"></a>網域同盟設定

下表描述要求主體中的必要和選擇性**DomainFederationSettings**屬性。

| 名稱   | 類型   | 必要項 | 描述                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | string           | 否      | 豐富型用戶端所使用的登入 URI。 這是合作夥伴的 STS 驗證 URL。 |
| DefaultInteractiveAuthenticationMethod | string           | 否      | 指出當應用程式需要使用者進行互動式登入時，應使用的預設驗證方法。 |
| FederationBrandName                    | string           | 否      | 同盟品牌名稱。        |
| IssuerUri                              | string           | 是     | 憑證的簽發者名稱。                        |
| LogOffUri                              | string           | 是     | 登出 URI。 這會描述同盟網域登出 URI。        |
| MetadataExchangeUri                    | string           | 否      | URL，指定用於從豐富型用戶端應用程式進行驗證的中繼資料交換端點。 |
| NextSigningCertificate                 | string           | 否      | ADFS V2 STS 用來簽署宣告的未來所用的憑證。 這是憑證的 base64 編碼標記法。 |
| OpenIdConnectDiscoveryEndpoint         | string           | 否      | 同盟 IDP STS 的 OpenID Connect 探索端點。 |
| PassiveLogOnUri                        | string           | 是     | 較舊的被動用戶端所使用的登入 URI。 這是傳送同盟登入要求的位址。 |
| PreferredAuthenticationProtocol        | string           | 是     | 驗證 token 的格式。 例如，"WsFed"。 支援的值： WsFed、Samlp |
| PromptLoginBehavior                    | string           | 是     | 提示登入行為類型。  例如，"TranslateToFreshPasswordAuth"。 支援的值： TranslateToFreshPasswordAuth、NativeSupport、Disabled |
| SigningCertificate                     | string           | 是     | ADFS V2 STS 目前用來簽署宣告的憑證。 這是憑證的 base64 編碼標記法。 |
| SigningCertificateUpdateStatus         | string           | 否      | 表示簽署憑證的更新狀態。 |
| SigningCertificateUpdateStatus         | 可為 null 的布林值 | 否      | 指出 IDP STS 是否支援 MFA。 支援的值： True、False、Null。|

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "Example.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capability": "Email",
        "IsDefault": Null,
        "IsInitial": Null,
        "Name": "Example.com",
        "RootDomain": null,
        "Status": "Verified",
        "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "Example.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed",
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此 API 會傳回新的已驗證網域的[網域](#domain)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 201 Created
Content-Length: 206
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "authenticationType": "federated",
    "capability": "email",
    "isDefault": false,
    "isInitial": false,
    "name": "Example.com",
    "status": "verified",
    "verificationMethod": "dns_record"
}
```