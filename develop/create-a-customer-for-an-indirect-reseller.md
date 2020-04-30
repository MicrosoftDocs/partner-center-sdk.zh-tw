---
title: 建立間接轉銷商的客戶
description: 間接提供者可以建立間接轉銷商的客戶。
ms.assetid: F6196EE1-1B72-4D0A-BE6E-56A243671CDE
ms.date: 06/03/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f67dcd1bfa2e3f896e2fb1e9ae777ef3974e22eb
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155210"
---
# <a name="create-a-customer-for-an-indirect-reseller"></a>建立間接轉銷商的客戶

**適用於：**

- 合作夥伴中心

間接提供者可以建立間接轉銷商的客戶。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 間接轉銷商的租使用者識別碼。

- 間接轉銷商必須與間接提供者合作。

## <a name="c"></a>C\#

為間接轉銷商新增客戶：

1. 具現化新的[**Customer**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer)物件，然後具現化並填入[**BillingProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile)和[**CompanyProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)。 請務必將間接轉銷商識別碼指派給[**AssociatedPartnerID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)屬性。

2. 使用 [ [**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) ] 屬性可取得客戶集合作業的介面。

3. 呼叫[**create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)方法以建立客戶。

### <a name="c-example"></a>C\#範例

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                       |
|----------|-------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的必要屬性。

| 名稱                                          | 類型   | 必要 | 描述                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | 物件 | 是      | 客戶的帳單設定檔資訊。                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | 物件 | 是      | 客戶的公司設定檔資訊。                                                                                                                                                                                                                                                                                                           |
| [AssociatedPartnerId](customer-resources.md#customer) | 字串 | 是      | 間接轉銷商識別碼。 如這裡提供的識別碼所指出的間接轉銷商，必須與間接提供者合作，否則要求將會失敗。 另請注意，如果未提供 AssociatedPartnerId 值，則會將客戶建立為間接提供者的直接客戶，而不是間接轉銷商。 |

#### <a name="billing-profile"></a>帳單設定檔

下表描述建立新客戶所需的[CustomerBillingProfile](customer-resources.md#customerbillingprofile)資源所需的最低欄位。

| 名稱             | 類型                                     | 必要 | 描述                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 電子郵件            | 字串                                   | 是      | 客戶的電子郵件地址。                                                                                                                                                                                   |
| culture          | 字串                                   | 是      | 其慣用的通訊和貨幣文化特性，例如 "en-us"。 請參閱[合作夥伴中心支援的語言和地區](partner-center-supported-languages-and-locales.md)設定以取得支援的文化特性。 |
| 語言         | 字串                                   | 是      | 預設語言。 支援兩個字元語言代碼（ `en`例如`fr`或）。                                                                                                                                |
| 公司\_名稱    | 字串                                   | 是      | 已註冊的公司/組織名稱。                                                                                                                                                                       |
| 預設\_位址 | [位址](utility-resources.md#address) | 是      | 客戶的公司/組織註冊的位址。 如需任何長度限制的資訊，請參閱[位址](utility-resources.md#address)資源。                                             |

#### <a name="company-profile"></a>公司設定檔

下表描述建立新客戶所需的[CustomerCompanyProfile](customer-resources.md#customercompanyprofile)資源所需的最低欄位。

| 名稱   | 類型   | 必要 | 描述                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| 網域 | 字串 | .是的     | 客戶的網域名稱，例如 contoso.onmicrosoft.com |

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，回應會包含新客戶的[客戶](customer-resources.md#customer)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```