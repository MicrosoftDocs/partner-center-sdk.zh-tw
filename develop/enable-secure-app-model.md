---
title: 啟用安全應用程式模型
description: 保護您的合作夥伴中心與控制台應用程式。
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0a6c3d14ca55350db832c10956b0751acb8f8a0c
ms.sourcegitcommit: 0dea06cd7f95026d93f970d3c294370a58dfcb6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2020
ms.locfileid: "76723190"
---
# <a name="enabling-the-secure-application-model-framework"></a>啟用安全應用程式模型架構

適用於：

- 合作夥伴中心

Microsoft 引進了一個安全、可擴充的架構，可透過 Microsoft Azure 多重要素驗證（MFA）架構來驗證雲端解決方案提供者（CSP）合作夥伴和控制台廠商（CPV）。

您可以使用新的模型來提升合作夥伴中心 API 整合呼叫的安全性。 這會協助所有的合作物件（包括 Microsoft、CSP 合作夥伴和 CPVs）保護其基礎結構和客戶資料免于安全性風險。

## <a name="scope"></a>領域

本主題涉及下列動作專案：

- CPVs
  - CPV 是獨立軟體廠商，其會開發應用程式，供 CSP 合作夥伴用來與合作夥伴中心 Api 整合。
  - CPV 不是可直接存取合作夥伴中心儀表板或 Api 的 CSP 合作夥伴。
- CSP 間接提供者和 CSP 直接合作夥伴，他們使用應用程式識別碼 + 使用者驗證，並直接與合作夥伴中心 Api 整合。

## <a name="security-requirements"></a>安全性需求

如需安全性需求的詳細資訊，請參閱[合作夥伴安全性需求](https://docs.microsoft.com/partner-center/partner-security-requirements)。

## <a name="secure-application-model"></a>安全應用程式模型

Marketplace 應用程式需要模擬 CSP 合作夥伴許可權，才能呼叫 Microsoft Api。 這些機密應用程式的安全性攻擊可能會導致客戶資料洩漏。

如需新驗證架構的總覽和詳細資訊，請下載[安全的應用程式模型架構](https://assetsprod.microsoft.com/secure-application-model-guide.pdf)檔。 本檔涵蓋的原則和最佳作法，是為了讓 marketplace 應用程式可持續且穩定于安全性危害。

## <a name="samples"></a>範例

下列總覽檔和範例程式碼會說明合作夥伴如何執行安全的應用程式模型架構：

- [CPV 總覽檔](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [CSP 總覽檔](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET 範例](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [JAVA 範例](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

- [REST 指示和範例](#rest)
- [PowerShell 指示和範例](#powershell)

## <a name="rest"></a>停

若要使用安全的應用程式模型架構進行 REST 呼叫，並搭配範例程式碼，您必須執行下列動作：

1. [建立 web 應用程式](#create-a-web-app)
2. [取得授權碼](#get-authorization-code)
3. [取得重新整理權杖](#get-refresh-token)
4. [取得存取權杖](#get-access-token)
5. [建立合作夥伴中心 API 呼叫](#make-partner-center-api-calls)

> [!TIP]
> 您可以使用合作夥伴中心 PowerShell 模組來取得授權碼和重新整理權杖。 您可以選擇此選項來取代步驟2和3。 如需詳細資訊，請參閱[PowerShell 一節和範例](#powershell)。

### <a name="create-a-web-app"></a>建立 web 應用程式

您必須先在合作夥伴中心建立並註冊 web 應用程式，才能進行 REST 呼叫。

1. 登入 [Azure 入口網站](https://portal.azure.com)。
2. 建立 Azure Active Directory （Azure AD）應用程式。
3. *根據您應用程式的需求*，授與委派的應用程式許可權給下列資源。 如有需要，您可以為應用程式資源新增更多委派的許可權。
    1. **Microsoft 合作夥伴中心**（某些租使用者顯示為**SampleBECApp**）
    2. **Azure 管理 api** （如果您打算呼叫 azure api）
    3. **Windows Azure Active Directory**
4. 請確定您應用程式的 [主 URL] 已設定為執行即時 web 應用程式的端點。 此應用程式將需要接受來自 Azure AD 登入呼叫的[授權碼](#get-authorization-code)。 例如，在[下一節](#get-authorization-code)的範例程式碼中，web 應用程式是在 `https://localhost:44395/`執行。
5. 請注意 Azure AD 中 web 應用程式設定的下列資訊：
    - 應用程式識別碼
    - 應用程式密碼

> [!NOTE]
> 建議[使用憑證做為您的應用程式密碼](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials)。 不過，您也可以在 Azure 入口網站中建立應用程式金鑰。 [下一節](#get-authorization-code)中的範例程式碼會使用應用程式金鑰。

### <a name="get-authorization-code"></a>取得授權碼

您必須取得 web 應用程式的授權碼，才能從 Azure AD 登入呼叫中接受：

1. 以下列 URL 登入 Azure AD： <https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1>。 請務必以您要用來進行合作夥伴中心 API 呼叫的使用者帳戶登入（例如，系統管理員代理程式或銷售代理程式帳戶）。
2. 將**應用程式識別碼**取代為您的 Azure AD 應用程式識別碼（GUID）。
3. 出現提示時，使用已設定 MFA 的使用者帳戶登入。
4. 出現提示時，請輸入其他 MFA 資訊（電話號碼或電子郵件地址）來驗證您的登入。
5. 登入之後，瀏覽器會使用您的授權碼將呼叫重新導向至您的 web 應用程式端點。 例如，下列範例程式碼會重新導向至 `https://localhost:44395/`。

#### <a name="authorization-code-call-trace"></a>授權碼呼叫追蹤

```http
POST https://localhost:44395/ HTTP/1.1
Origin: https://login.microsoftonline.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referrer: https://login.microsoftonline.com/kmsi
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: OpenIdConnect.nonce.hOMjjrivcxzuI4YqAw4uYC%2F%2BILFk4%2FCx3kHTHP3lBvA%3D=dHVyRXdlbk9WVUZFdlFONVdiY01nNEpUc0JRR0RiYWFLTHhQYlRGNl9VeXJqNjdLTGV3cFpIWFg1YmpnWVdQUURtN0dvMkdHS2kzTm02NGdQS09veVNEbTZJMDk1TVVNYkczYmstQmlKUzFQaTBFMEdhNVJGVHlES2d3WGlCSlVlN1c2UE9sd2kzckNrVGN2RFNULWdHY2JET3RDQUxSaXRfLXZQdG00RnlUM0E1TUo1YWNKOWxvQXRwSkhRYklQbmZUV3d3eHVfNEpMUUthMFlQUFgzS01RS2NvMXYtbnV4UVJOYkl4TTN0cw%3D%3D

code=AuthorizationCodeValue&id_token=IdTokenValue&<rest of properties for state>
```

### <a name="get-refresh-token"></a>取得重新整理權杖

接著，您必須使用您的授權碼來取得重新整理權杖：

1. 使用授權碼對 Azure AD 登入端點進行 POST 呼叫 `https://login.microsoftonline.com/CSPTenantID/oauth2/token`。 如需範例，請參閱下列[範例呼叫](#sample-refresh-call)。
2. 請注意傳回的重新整理權杖。
3. 在 Azure Key Vault 中儲存重新整理權杖。 如需詳細資訊，請參閱[KEY VAULT API 檔](https://docs.microsoft.com/rest/api/keyvault/)。

> [!IMPORTANT]
> 重新整理權杖必須以[秘密的形式儲存](https://docs.microsoft.com/rest/api/keyvault/setsecret/setsecret)在 Key Vault 中。

#### <a name="sample-refresh-call"></a>範例重新整理呼叫

預留位置要求：

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

要求本文：

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

預留位置回應：

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

回應主體：

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>取得存取權杖

您必須先取得存取權杖，才能對合作夥伴中心 Api 進行呼叫。 您必須使用重新整理權杖來取得存取權杖，因為存取權杖通常會有非常有限的存留期（例如，不到一小時）。

預留位置要求：

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

要求本文：

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

預留位置回應：

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

回應主體：

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>進行合作夥伴中心 API 呼叫

您必須使用存取權杖來呼叫合作夥伴中心 Api。 請參閱下列範例呼叫。

#### <a name="example-partner-center-api-call"></a>合作夥伴中心 API 呼叫範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

您可以使用[合作夥伴中心 PowerShell 模組](https://www.powershellgallery.com/packages/PartnerCenter)來減少所需的基礎結構，以交換存取權杖的授權碼。 這個方法是讓[合作夥伴中心 REST 呼叫](#rest)的選擇性方式。

如需此流程的詳細資訊，請參閱[保護應用程式模型](https://docs.microsoft.com/powershell/partnercenter/secure-app-model)PowerShell 檔。

1. 安裝 Azure AD 和合作夥伴中心的 PowerShell 模組。

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. 使用 **[PartnerAccessToken](https://docs.microsoft.com/powershell/module/partnercenter/new-partneraccesstoken)** 命令來執行同意程式，並捕捉所需的重新整理權杖。

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > **ServicePrincipal**參數會與**PartnerAccessToken**命令搭配使用，因為正在使用具有**Web/API**類型的 Azure AD 應用程式。 這種類型的應用程式要求用戶端識別碼和密碼必須包含在存取權杖要求中。 叫用**Get-Credential**命令時，系統會提示您輸入使用者名稱和密碼。 輸入應用程式識別碼做為使用者名稱。 輸入 [應用程式秘密] 做為密碼。 叫用**PartnerAccessToken**命令時，系統會提示您再次輸入認證。 輸入您所使用之服務帳戶的認證。 此服務帳戶應該是具有適當許可權的夥伴帳戶。

3. 複製 [重新整理權杖] 值。

    ```powershell
    $token.RefreshToken | clip
    ```

您應該將重新整理權杖值儲存在安全的儲存機制中，例如 Azure Key Vault。 如需如何利用 PowerShell 的安全應用程式模組的詳細資訊，請參閱[多因素驗證一](https://docs.microsoft.com/powershell/partnercenter/multi-factor-auth)文。
