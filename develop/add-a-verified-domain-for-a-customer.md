---
title: Add a verified domain for a customer
description: Add a verified domain to the list of approved domains for a customer in Partner Center.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f5abd926389c1c81a178fe5cd2476929070657f6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486218"
---
# <a name="add-a-verified-domain-for-a-customer"></a>Add a verified domain for a customer

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

How to add a verified domain to the list of approved domains for an existing customer.

## <a name="prerequisites"></a>必要條件

- You must be a Partner who is a domain registrar.
- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer ID (**CustomerTenantId**). If you don't have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting **Account**, then saving their Microsoft ID.

## <a name="adding-a-verified-domain"></a>Adding a verified domain

If you are a Partner who is a domain registrar, you can use the verifieddomain API to POST a new [Domain](#domain) resource to the list of domains for an existing customer. To do this, identify the customer using their CustomerTenantId, specify a value for the VerifiedDomainName property, and pass a [Domain](#domain) resource in the Request with the required Name, Capability, AuthenticationType, Status, and VerificationMethod properties included. To specify that the new [Domain](#domain) is a federated domain, set the AuthenticationType property in the [Domain](#domain) resource to "Federated", and include a [DomainFederationSettings](#domain-federation-settings) resource in the Request. If the method is successful, the Response will include a [Domain](#domain) resource for the new verified domain.

### <a name="custom-verified-domains"></a>Custom verified domains

When adding a custom verified domain, a domain that is not registered on **onmicrosoft.com**, you must set the [CustomerUser.immutableId](user-resources.md#customeruser) property to a unique ID value for the customer you are adding the domain for. This unique identifier is required during the validation process when the domain is being verified. For more information about customer user accounts, see [create user accounts for a customer](create-user-accounts-for-a-customer.md).

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |

#### <a name="uri-parameter"></a>URI 參數

Use the following query parameter to specify the customer you are adding a verified domain for.

| 名稱                   | 在工作列搜尋方塊中輸入     | 必要 | 說明                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer. |

### <a name="request-headers"></a>要求標頭

For more information, see [Partner Center REST headers](headers.md).

### <a name="request-body"></a>要求主體

This table describes the required properties in the request body.

| 名稱                                                  | 在工作列搜尋方塊中輸入   | 必要                                      | 說明                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | 字串 | [是]                                           | The verified domain name. |
| [網域](#domain)                                     | 物件 | [是]                                           | Contains the domain information. |
| [DomainFederationSettings](#domain-federation-settings) | 物件 | Yes (If AuthenticationType = "Federated")     | The domain federation settings to be used if the domain is a "Federated" domain and not a "Managed" domain. |

#### <a name="domain"></a>網域

This table describes the required and optional **Domain** properties in the request body.

| 名稱               | 在工作列搜尋方塊中輸入                                     | 必要 | 說明                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | 字串           | [是]      | Defines whether the domain is a "Managed" domain or a "Federated" domain. Supported values: Managed, Federated.|
| 功能                                            | 字串           | [是]      | Specifies the domain capability. For example, "Email".                  |
| IsDefault                                             | nullable boolean | 無       | Indicates whether the domain is the default domain for the tenant. Supported values: True, False, Null.        |
| IsInitial                                             | nullable boolean | 無       | Indicates whether the domain is an initial domain. Supported values: True, False, Null.                       |
| 名稱                                                  | 字串           | [是]      | The domain name.                                                          |
| RootDomain                                            | 字串           | 無       | The name of the root domain.                                              |
| 狀態                                                | 字串           | [是]      | The domain status. For example, "Verified". Supported values:  Unverified, Verified, PendingDeletion.                               |
| VerificationMethod                                    | 字串           | [是]      | The domain verification method type. Supported values: None, DnsRecord, Email.                                    |

##### <a name="domain-federation-settings"></a>Domain federation settings

This table describes the required and optional **DomainFederationSettings** properties in the request body.

| 名稱   | 在工作列搜尋方塊中輸入   | 必要 | 說明                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | 字串           | 無      | The logon URI used by rich clients. This is the partner's STS Auth URL. |
| DefaultInteractiveAuthenticationMethod | 字串           | 無      | Indicates the default authentication method that should be used when an application requires the user to have interactive login. |
| FederationBrandName                    | 字串           | 無      | The federation brand name.        |
| IssuerUri                              | 字串           | [是]     | The name of the issuer of the certificates.                        |
| LogOffUri                              | 字串           | [是]     | The logoff URI. This describes the federated domain sign-out URI.        |
| MetadataExchangeUri                    | 字串           | 無      | The URL that specifies the metadata exchange endpoint used for authentication from rich client applications. |
| NextSigningCertificate                 | 字串           | 無      | The certificate used for the coming future by the ADFS V2 STS to sign claims. This is a base64 encoded representation of the certificate. |
| OpenIdConnectDiscoveryEndpoint         | 字串           | 無      | The OpenID Connect Discovery Endpoint of the federated IDP STS. |
| PassiveLogOnUri                        | 字串           | [是]     | The logon URI used by older passive Clients. This is the address to send federated sign-in requests. |
| PreferredAuthenticationProtocol        | 字串           | [是]     | The format for the authentication token. For example, "WsFed". Supported values: WsFed, Samlp |
| PromptLoginBehavior                    | 字串           | [是]     | The prompt login behavior type.  For example, "TranslateToFreshPasswordAuth". Supported values: TranslateToFreshPasswordAuth, NativeSupport, Disabled |
| SigningCertificate                     | 字串           | [是]     | The certificate currently used by the ADFS V2 STS to sign claims. This is a base64 encoded representation of the certificate. |
| SigningCertificateUpdateStatus         | 字串           | 無      | Indicates the update status of the Signing certificate. |
| SigningCertificateUpdateStatus         | nullable boolean | 無      | Indicates whether the IDP STS supports MFA. Supported values: True, False, Null.|

### <a name="request-example"></a>要求的範例

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

## <a name="rest-response"></a>REST response

If successful, this API returns a [Domain](#domain) resource for the new verified domain.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

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