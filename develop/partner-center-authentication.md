---
title: 合作夥伴中心驗證
description: 合作夥伴中心會使用 Azure AD 進行驗證，並使用合作夥伴中心 Api，您必須正確地設定驗證設定。
ms.assetid: 2307F2A8-7BD4-4442-BEF7-F065F16DA0B2
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7a29d178774f301f5f3030df119bf30953fa0d8f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486978"
---
# <a name="partner-center-authentication"></a>合作夥伴中心驗證

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心會利用 Azure Active Directory 來進行驗證。 與合作夥伴中心 API、SDK 或 PowerShell 模組互動時，您必須正確地設定 Azure AD 應用程式，然後要求存取權杖。 使用 [僅限應用程式] 或 [應用程式 + 使用者驗證] 取得的存取權杖可與合作夥伴中心搭配使用。 不過，有兩個需要考慮的重要專案

- 使用應用程式 + 使用者驗證存取合作夥伴中心 API 時，您必須使用多重要素驗證。 若要尋找有關此變更的詳細資訊，請參閱[啟用安全應用程式模型](enable-secure-app-model.md)
- 合作夥伴中心 API 不支援僅限應用程式驗證的所有作業。 這表示在某些情況下，您需要使用應用程式 + 使用者驗證。 在每個[案例](https://docs.microsoft.com/partner-center/develop/scenarios)文章的*必要條件*標題底下，您會找到說明是否支援僅限應用程式驗證、應用程式 + 使用者驗證或兩者的檔。

## <a name="initial-setup"></a>初始設定

1. 若要開始，您必須確定您有主要合作夥伴中心帳戶，以及整合沙箱合作夥伴中心帳戶。 如需詳細資訊，請參閱[設定 API 存取的合作夥伴中心帳戶](set-up-api-access-in-partner-center.md)。 請記下您主要帳戶和整合沙箱帳戶的 Azure AAD 應用程式註冊識別碼和密碼（僅限應用程式識別所需的用戶端密碼）。

2. 從 Azure 管理入口網站登入 Azure AD。 在 **其他應用程式的許可權** 中，將  **Windows Azure Active Directory**的許可權設定為 **委派的許可權**，然後選取 以登**入使用者身分存取目錄** 和 登**入及讀取使用者設定檔**。

3. 在 Azure 管理入口網站中，**新增應用程式**。 搜尋「Microsoft 合作夥伴中心」，也就是 Microsoft 合作夥伴中心應用程式。 設定**委派的許可權**以**存取合作夥伴中心 API**。 如果您使用合作夥伴中心來 Microsoft Cloud 德國或合作夥伴中心用於美國政府的 Microsoft Cloud，則此為必要步驟。 如果您使用合作夥伴中心的全域實例，此步驟是選擇性的。 CSP 合作夥伴可以使用合作夥伴中心入口網站中的應用程式管理功能，針對合作夥伴中心的全域實例略過此步驟。

## <a name="app-only-authentication"></a>僅限應用程式的驗證

如果您想要使用僅限應用程式的驗證來存取合作夥伴中心 REST API、.NET API、JAVA API 或 PowerShell 模組，則可以利用下列指示來執行此動作。

### <a name="net-app-only-authentication"></a>.NET （僅限應用程式驗證）

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials =
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId,
            PartnerApplicationConfiguration.ApplicationSecret,
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

### <a name="java-app-only-authentication"></a>JAVA （僅限應用程式驗證）

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(),
        PartnerApplicationConfiguration.getApplicationSecret(),
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

### <a name="rest-app-only-authentication"></a>REST （僅限應用程式驗證）

#### <a name="rest-request"></a>REST 要求

```http
POST https://login.microsoftonline.com/{tenantId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

#### <a name="rest-response"></a>REST 回應

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>應用程式 + 使用者驗證

在過去，[資源擁有者密碼認證授](https://tools.ietf.org/html/rfc6749#section-4.3)與已用來要求存取權杖，以與合作夥伴中心 REST API、.net Api、JAVA Api 或 PowerShell 模組搭配使用。 這是您從 Azure Active Directory 使用用戶端識別碼和使用者認證要求存取權杖的位置。 此方法將不再有效，因為合作夥伴中心在使用應用程式 + 使用者驗證時需要多重要素驗證。 為了符合這項需求，Microsoft 引進了一個安全、可擴充的架構，可使用多重要素驗證來驗證雲端解決方案提供者（CSP）合作夥伴和控制台廠商（CPV）。 此架構稱為安全應用程式模型，它是由同意程式和使用重新整理權杖的存取權杖要求所組成。

### <a name="partner-consent"></a>合作夥伴同意

夥伴同意程式是一種互動式程式，其中合作夥伴會使用多重要素驗證進行驗證、同意至應用程式，而重新整理權杖會儲存在安全的儲存機制中，例如 Azure Key Vault。 我們建議針對此程式使用整合用途的專用帳戶。

> [!IMPORTANT]  
> 應針對合作夥伴同意程式中所使用的服務帳戶啟用適當的多重要素驗證解決方案。 如果不是，則產生的重新整理權杖將不符合安全性需求。

### <a name="samples-for-app--user-authentication"></a>應用程式 + 使用者驗證的範例

您可以透過數種方式來執行合作夥伴同意流程。 為了協助合作夥伴瞭解如何執行每項必要的作業，我們開發了下列範例。 請注意，這些僅為範例。 當您在環境中執行適當的解決方案時，請務必開發符合編碼標準和安全性原則的解決方案。

### <a name="net-appuser-authentication"></a>.NET （應用程式 + 使用者驗證）

[合作夥伴同意](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault)範例專案會示範如何利用使用 ASP.NET 開發的網站來捕捉同意、要求重新整理權杖，並將它安全地儲存在 Azure Key Vault 中。 請執行下列步驟，以建立此範例所需的必要條件。

1. 使用 Azure 管理入口網站或下列 PowerShell 命令，建立 Azure Key Vault 的實例。 執行命令之前，請務必據以修改參數值。 保存庫名稱必須是唯一的。

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    如果您需要建立實例 Azure Key Vault 的說明，請參閱[快速入門：從 Azure Key Vault 設定和取出秘密使用 Azure 入口網站](https://docs.microsoft.com/azure/key-vault/quick-create-portal)或[快速入門：使用 PowerShell 從 Azure Key Vault 設定和取出秘密](https://docs.microsoft.com/azure/key-vault/quick-create-powershell)，以取得如何建立 Azure Key Vault 實例的逐步指示，然後設定和取出秘密。

2. 使用 Azure 管理入口網站或下列命令，建立 Azure AD 應用程式和金鑰。

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    請務必記下 [應用程式識別碼] 和 [密碼] 值，因為它們將用於下列步驟中。

3. 使用 Azure 管理入口網站或下列命令，為新建立的 Azure AD 應用程式授與讀取秘密許可權。

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. 建立針對合作夥伴中心設定的 Azure AD 應用程式。 執行下列動作以完成此步驟。

    - 流覽至合作夥伴中心儀表板的[應用程式管理](https://partner.microsoft.com/pcv/apiintegration/appmanagement)功能
    - 按一下 [*新增 web 應用*程式] 以建立新的 Azure AD 應用程式。

    請務必記載 [*應用程式識別碼*]、[帳戶識別碼] * * 和 [*金鑰*] 值，因為它們將用於下列步驟中。

5. 使用 Visual Studio 或下列命令來複製[合作夥伴中心-DotNet 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)存放庫。

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. 開啟 `Partner-Center-DotNet-Samples\secure-app-model\keyvault` 目錄中找到的*PartnerConsent*專案。
7. 填入[在 web.config 中](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)找到的應用程式設定

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!-- 
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- 
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!-- 
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]  
    > 敏感性資訊（例如應用程式秘密）不應儲存在設定檔中。 因為這是一個範例應用程式，所以是在這裡完成的。 在您的生產應用程式中，我們強烈建議您使用以憑證為基礎的驗證。 如需詳細資訊，請參閱[憑證認證以取得應用程式驗證](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials)。

8. 當您執行這個範例專案時，它會提示您進行驗證。 成功驗證之後，會從 Azure AD 要求存取權杖。 從 Azure AD 傳回的資訊包含重新整理權杖，此標記儲存在 Azure Key Vault 設定的實例中。  

### <a name="java-appuser-authentication"></a>JAVA （應用程式 + 使用者驗證）

[合作夥伴同意](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault)範例專案會示範如何利用使用 JSP 開發的網站來捕捉同意、要求重新整理權杖，以及 Azure Key Vault 中的安全存放區。 執行下列動作，以建立此範例所需的必要條件。

1. 使用 Azure 管理入口網站或下列 PowerShell 命令，建立 Azure Key Vault 的實例。 執行命令之前，請務必據以修改參數值。 保存庫名稱必須是唯一的。

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    如果您需要建立實例 Azure Key Vault 的說明，請參閱[快速入門：從使用 Azure 入口網站或快速入門的 Azure Key Vault 設定和取出秘密](https://docs.microsoft.com/azure/key-vault/quick-create-portal)。如需如何建立 Azure Key Vault 實例及設定和抓取秘密的逐步指示，請參閱[使用 PowerShell 從 Azure Key Vault 設定](https://docs.microsoft.com/azure/key-vault/quick-create-powershell)和取出秘密。

2. 使用 Azure 管理入口網站或下列命令，建立 Azure AD 應用程式和金鑰。

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    請務必記載應用程式識別碼和密碼值，因為它們將用於下列步驟中。

3. 使用 Azure 管理入口網站或下列命令，將 [讀取秘密] 許可權授與新建立的 Azure AD 應用程式。

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. 建立針對合作夥伴中心設定的 Azure AD 應用程式。 請執行下列各項，以完成此步驟。

    - 流覽至合作夥伴中心儀表板的[應用程式管理](https://partner.microsoft.com/pcv/apiintegration/appmanagement)功能
    - 按一下 [*新增 web 應用*程式] 以建立新的 Azure AD 應用程式。

    請務必記載 [*應用程式識別碼*]、[帳戶識別碼] * * 和 [*金鑰*] 值，因為它們將用於下列步驟中。

5. 使用下列命令複製[合作夥伴中心-JAVA 範例](https://github.com/Microsoft/Partner-Center-Java-Samples)存放庫

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. 開啟 `Partner-Center-Java-Samples\secure-app-model\keyvault` 目錄中找到的*PartnerConsent*專案。
7. 填入在[web .xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)檔案中找到的應用程式設定

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]  
    > 敏感性資訊（例如應用程式秘密）不應儲存在設定檔中。 因為這是一個範例應用程式，所以是在這裡完成的。 在您的生產應用程式中，我們強烈建議您使用以憑證為基礎的驗證。 如需詳細資訊，請參閱[Key Vault 憑證驗證](https://github.com/Azure-Samples/key-vault-java-certificate-authentication)。

8. 當您執行這個範例專案時，它會提示您進行驗證。 成功驗證之後，會從 Azure AD 要求存取權杖。 從 Azure AD 傳回的資訊包含重新整理權杖，此標記儲存在 Azure Key Vault 設定的實例中。  

## <a name="cloud-solution-provider-authentication"></a>雲端解決方案提供者驗證

雲端解決方案提供者合作夥伴可以使用透過[合作夥伴同意](#partner-consent)流程取得的重新整理權杖。

### <a name="samples-for-cloud-solution-provider-authentication"></a>雲端解決方案提供者驗證的範例

為了協助合作夥伴瞭解如何執行每項必要的作業，我們開發了下列範例。 請注意，這些僅為範例。 當您在環境中執行適當的解決方案時，請務必開發符合編碼標準和安全性原則的解決方案。

### <a name="net-csp-authentication"></a>.NET （CSP 驗證）

1. 如果您尚未這麼做，請執行[合作夥伴同意流程](#partner-consent)。
2. 使用 Visual Studio 或下列命令複製[合作夥伴中心-DotNet 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)存放庫

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. 開啟在 `Partner-Center-DotNet-Samples\secure-app-model\keyvault` 目錄中找到的 `CSPApplication` 專案。
4. 更新[app.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config)檔案中找到的應用程式設定。

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!-- 
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!-- 
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. 為[Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)檔案中找到的**PartnerId**和**CustomerId**變數設定適當的值。

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. 當您執行這個範例專案時，它會取得在合作夥伴同意程式期間取得的重新整理權杖。 然後，它會要求存取權杖，以代表合作夥伴與合作夥伴中心 SDK 互動。 最後，它會要求存取權杖，以代表指定的客戶與 Microsoft Graph 互動。

### <a name="java-csp-authentication"></a>JAVA （CSP 驗證）

1. 如果您尚未這麼做，請執行[合作夥伴同意流程](#partner-consent)。
2. 使用 Visual Studio 或下列命令複製[合作夥伴中心-JAVA 範例](https://github.com/Microsoft/Partner-Center-Java-Samples)存放庫

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. 開啟在 `Partner-Center-Java-Samples\secure-app-model\keyvault` 目錄中找到的 `cspsample` 專案。
4. 更新在[應用程式. properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties)檔案中找到的應用程式設定。

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. 當您執行這個範例專案時，它會取得在合作夥伴同意程式期間取得的重新整理權杖。 然後，它會要求存取權杖，以代表合作夥伴與合作夥伴中心 SDK 互動。
6. 選擇性-如果您想要瞭解如何與 Azure Resource Manager 進行互動，並代表客戶 Microsoft Graph，請取消批註*RunAzureTask*和*RunGraphTask*函式呼叫。

## <a name="control-panel-provider-authentication"></a>控制台提供者驗證

「控制台」廠商必須讓他們支援的每個合作夥伴都執行[合作夥伴同意](#partner-consent)流程。 完成後，會使用透過該程式取得的重新整理權杖來存取合作夥伴中心 REST API 和 .NET API。

### <a name="samples-for-cloud-panel-provider-authentication"></a>雲端面板提供者驗證的範例

為了協助「控制台」廠商瞭解如何執行每項必要的作業，我們開發了下列範例。 請注意，這些僅為範例。 當您在環境中執行適當的解決方案時，請務必開發符合編碼標準和安全性原則的解決方案。

### <a name="net-cpv-authentication"></a>.NET （CPV authentication）

1. 為雲端解決方案提供者合作夥伴開發及部署流程，以提供適當的同意。 如需其他詳細資料和範例，請參閱[合作夥伴同意](#partner-consent)。

    > [!IMPORTANT]  
    > 不應儲存來自雲端解決方案提供者合作夥伴的使用者認證。 透過合作夥伴同意程式取得的重新整理權杖應加以儲存，並用來要求存取權杖，以便與任何 Microsoft API 互動。

2. 使用 Visual Studio 或下列命令複製[合作夥伴中心-DotNet 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)存放庫

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. 開啟在 `Partner-Center-DotNet-Samples\secure-app-model\keyvault` 目錄中找到的 `CPVApplication` 專案。
4. 更新[app.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config)檔案中找到的應用程式設定。

    ```xml
    <!-- AppID that represents Control panel vendor application -->
    <add key="ida:CPVApplicationId" value="" />

    <!-- 
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:CPVApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!-- 
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. 為[Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)檔案中找到的**PartnerId**和**CustomerId**變數設定適當的值。

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. 當您執行這個範例專案時，它會取得指定之夥伴的重新整理權杖。 然後，它會要求存取權杖以存取合作夥伴中心，並代表合作夥伴 Azure AD 圖形。 它所執行的下一個工作是在客戶租使用者中刪除和建立許可權授與。 由於「控制台」廠商與客戶之間沒有任何關聯性，因此必須使用合作夥伴中心 API 來新增這些許可權。 下列範例顯示如何完成這項作業。

    ```csharp
    JObject contents = new JObject
    {
        // Provide your application display name
        ["displayName"] = "CPV Marketplace",

        // Provide your application id
        ["applicationId"] = CPVApplicationId,

        // Provide your application grants
        ["applicationGrants"] = new JArray(
            JObject.Parse("{\"enterpriseApplicationId\": \"00000002-0000-0000-c000-000000000000\", \"scope\":\"Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All\"}"), // for Azure AD Graph access,  Directory.Read.All
            JObject.Parse("{\"enterpriseApplicationId\": \"797f4846-ba00-4fd7-ba43-dac1f8f63013\", \"scope\":\"user_impersonation\"}")) // for Azure Resource Manager access
    };

    /**
     * The following steps have to be performed once per customer tenant if your application is
     * a control panel vendor application and requires customer tenant Azure AD Graph access.
     **/

    // delete the previous grant into customer tenant
    JObject consentDeletion = await ApiCalls.DeleteAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents/{1}", CustomerId, CPVApplicationId));

    // create new grants for the application given the setting in application grants payload.
    JObject consentCreation = await ApiCalls.PostAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents", CustomerId),
        contents.ToString());
    ```

建立這些許可權之後，範例會代表客戶使用 Azure AD 圖形來執行作業。

### <a name="java-cpv-authentication"></a>JAVA （CPV authentication）

1. 為雲端解決方案提供者合作夥伴開發及部署流程，以提供適當的同意。 如需其他詳細資料和範例，請參閱[合作夥伴同意](#partner-consent)。

    > [!IMPORTANT]  
    > 不應儲存來自雲端解決方案提供者合作夥伴的使用者認證。 透過合作夥伴同意程式取得的重新整理權杖應加以儲存，並用來要求存取權杖，以便與任何 Microsoft API 互動。

2. 使用下列命令複製[合作夥伴中心-JAVA 範例](https://github.com/Microsoft/Partner-Center-Java-Samples)存放庫

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. 開啟在 `Partner-Center-Java-Samples\secure-app-model\keyvault` 目錄中找到的 `cpvsample` 專案。
4. 更新在[應用程式. properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties)檔案中找到的應用程式設定。

    ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    partnercenter.displayName=
    ```

    `partnercenter.displayName` 的值應該是 marketplace 應用程式的顯示名稱。

5. 針對[Program. java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java)檔案中找到的**partnerId**和**customerId**變數設定適當的值。

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. 當您執行這個範例專案時，它會取得指定之夥伴的重新整理權杖。 然後，它會要求存取權杖，以代表合作夥伴存取合作夥伴中心。 它所執行的下一個工作是在客戶租使用者中刪除和建立許可權授與。 由於「控制台」廠商與客戶之間沒有任何關聯性，因此必須使用合作夥伴中心 API 來新增這些許可權。 下列範例顯示如何完成這項作業。

    ```java
    ApplicationGrant azureAppGrant = new ApplicationGrant();

    azureAppGrant.setEnterpriseApplication("797f4846-ba00-4fd7-ba43-dac1f8f63013");
    azureAppGrant.setScope("user_impersonation");

    ApplicationGrant graphAppGrant = new ApplicationGrant();

    graphAppGrant.setEnterpriseApplication("00000002-0000-0000-c000-000000000000");
    graphAppGrant.setScope("Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All");

    ApplicationConsent consent = new ApplicationConsent();

    consent.setApplicationGrants(Arrays.asList(azureAppGrant, graphAppGrant));
    consent.setApplicationId(properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID));
    consent.setDisplayName(properties.getProperty(PropertyName.PARTNER_CENTER_DISPLAY_NAME));

    // Deletes the existing grant into the customer it is present.
    partnerOperations.getServiceClient().delete(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents/{1}",
            customerId,
            properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID)));

    // Consent to the defined applications and the respective scopes.
    partnerOperations.getServiceClient().post(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents",
            customerId),
        consent);
    ```

如果您想要瞭解如何與 Azure Resource Manager 進行互動，並代表客戶 Microsoft Graph，請取消批註*RunAzureTask*和*RunGraphTask*函式呼叫。
