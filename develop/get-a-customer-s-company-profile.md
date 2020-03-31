---
title: 取得客戶的公司設定檔
description: 取得客戶的公司設定檔。
ms.assetid: 762C0F38-2229-464D-9CD6-6AD82135A65C
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a2d011e425d4fac1eeb2efdd530c6bab312c63c6
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415597"
---
# <a name="get-a-customers-company-profile"></a>取得客戶的公司設定檔

**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得客戶的公司設定檔。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>範例

### <a name="c"></a>C#

若要取得客戶的公司設定檔，請呼叫[**iaggregatepartner.customers.byid 的 ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，並提供客戶識別碼來識別客戶。 然後從 [[**設定檔**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles)] 屬性取得客戶的[**ICustomerProfileCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection)介面，以便存取其公司屬性。 接下來，從[**ICustomerProfileCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company)屬性取得[**ICustomerReadonlyProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1)介面，並呼叫其[**get （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get)或[**GetAsync （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)方法。

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

**範例**：[下載合作夥伴中心 SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681)。 **專案**： PartnerSdk. FeatureSamples**類別**： GetCustomerCompanyProfile.cs

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

若要取得客戶的公司設定檔，請使用客戶識別碼呼叫**iaggregatepartner.customers.byid. getCustomers （）. byId**函數來識別客戶。 然後從 [**ipartner.getprofiles**] 函數取得客戶的**ICustomerProfileCollection**介面，以便存取其公司屬性。 接下來，從**ICustomerProfileCollection getCompany**函式取得**ICustomerReadonlyProfile**介面，並呼叫**get**函式。

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求

**要求語法**

| 方法  | 要求 URI                                                             |
|---------|-------------------------------------------------------------------------|
| **GET** | *{baseURL}* /v1/customers/{customer-tenant-id}/profiles/company HTTP/1。1 |

**URI 參數**

使用下列查詢參數來取得公司設定檔。

| 名稱                   | 類型     | 必要項 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。 |


**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

無

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，此方法會在回應主體中傳回信息。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```