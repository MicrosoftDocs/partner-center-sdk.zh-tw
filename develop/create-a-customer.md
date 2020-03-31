---
title: 建立客戶
description: 如何建立新的客戶。
ms.assetid: 7EA3E23F-0EA8-49CB-B98A-C4B74F559873
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: bf9007c4f3750b66326475e15479006c87e9f6a7
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413491"
---
# <a name="create-a-customer"></a>建立客戶

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本主題說明如何建立新的客戶。

> [!IMPORTANT]
> 如果您是間接提供者，而且想要建立間接轉銷商的客戶，請參閱[建立間接轉銷](create-a-customer-for-an-indirect-reseller.md)商的客戶。

身為雲端解決方案提供者（CSP）合作夥伴，當您建立客戶時，您可以代表客戶來放置訂單。 當您建立客戶時，您也會建立：

- 客戶的 Azure Active Directory （AD）租使用者物件。
- 轉銷商與客戶之間的關聯性，用於委派的系統管理員許可權。
- 用來以系統管理員身分登入客戶的使用者名稱和密碼。

建立客戶之後，請務必儲存客戶識別碼，並 Azure AD 詳細資料，以供日後用於合作夥伴中心 SDK （例如，帳戶管理）。

## <a name="prerequisites"></a>必要條件

認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

> [!IMPORTANT]
> 若要建立客戶租使用者，您必須在建立程式期間提供有效的實體位址。 您可以遵循[驗證位址](validate-an-address.md)案例中所述的步驟來驗證位址。 如果您在沙箱環境中使用不正確位址建立客戶，就無法刪除該客戶租使用者。

## <a name="c"></a>C\#

若要新增客戶：

1. 具現化新的[**Customer**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer)物件。 請務必填寫[**BillingProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile)和[**CompanyProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)。
2. 藉由呼叫[**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)，將新客戶新增至您的[**iaggregatepartner.customers.byid 客戶**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers)集合。

### <a name="c-example"></a>C\# 範例

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

若要建立新的客戶：

1. 建立**CustomerBillingProfile**的新實例和**CustomerCompanyProfile**物件。 請務必填入必要欄位。
2. 呼叫**iaggregatepartner.customers.byid. getCustomers （）. create** function 來建立客戶。

### <a name="java-example"></a>JAVA 範例

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

若要建立客戶，請執行[**PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)命令。

### <a name="powershell-example"></a>Powershell 範例

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                       |
|----------|-------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

- 此 API 具有等冪性（如果您多次呼叫，則不會產生不同的結果）。
- 需要要求識別碼和相互關聯識別碼。
- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的必要屬性。

| 名稱                              | 類型   | 描述                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | object | 客戶的帳單設定檔資訊。 |
| [CompanyProfile](#company-profile) | object | 客戶的公司設定檔資訊。 |

#### <a name="billing-profile"></a>帳單設定檔

下表描述建立新客戶所需的[CustomerBillingProfile](customer-resources.md#customerbillingprofile)資源所需的最低欄位。

| 名稱             | 類型                                     | 描述                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 電子郵件            | string                                   | 客戶的電子郵件地址。                                                                                                                                                                                   |
| culture (文化特性)          | string                                   | 其慣用的通訊和貨幣文化特性，例如 "en-us"。 請參閱[合作夥伴中心支援的語言和地區](partner-center-supported-languages-and-locales.md)設定以取得支援的文化特性。 |
| 語言         | string                                   | 預設語言。 支援兩個字元語言代碼（例如 en、fr）。                                                                                                                                |
| 公司\_名稱    | string                                   | 已註冊的公司/組織名稱。                                                                                                                                                                       |
| 預設\_位址 | [地址](utility-resources.md#address) | 客戶的公司/組織註冊的位址。 如需任何長度限制的資訊，請參閱[位址](utility-resources.md#address)資源。                                             |

#### <a name="company-profile"></a>公司設定檔

下表描述建立新客戶所需的[CustomerCompanyProfile](customer-resources.md#customercompanyprofile)資源所需的最低欄位。

| 名稱   | 類型   | 描述                                                  |
|--------|--------|--------------------------------------------------------------|
| domain | string | 客戶的功能變數名稱，例如 contoso.onmicrosoft.com。 |

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此 API 會傳回新客戶的[客戶](customer-resources.md#customer)資源。 儲存客戶識別碼並 Azure AD 詳細資料，以供未來與合作夥伴中心 SDK 搭配使用。 例如，您將需要這些專案才能與帳戶管理搭配使用。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
