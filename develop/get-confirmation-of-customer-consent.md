---
title: Get confirmation of customer acceptance of Microsoft Cloud Agreement
description: This topic explains how to get confirmation of customer acceptance of the Microsoft Cloud Agreement.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9ae40cd3c9805ee8ddaae6d98fd0d6b61ede8d40
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485658"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>取得客戶接受 Microsoft Cloud 合約的確認

**Applies To**

- 合作夥伴中心

> [!NOTE]  
> The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> - 由 21Vianet 營運的合作夥伴中心
> - Microsoft Cloud 德國合作夥伴中心
> - Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="prerequisites"></a>必要條件

- If you are using the Partner Center .NET SDK, version 1.9 or newer is required.
- If you are using the Partner Center Java SDK, version 1.8 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports only supports app + user authentication.
- A customer ID (customer-tenant-id).

## <a name="net-version-14-or-newer"></a>.NET (version 1.4 or newer)

To retrieve confirmation(s) of customer acceptance that was previously provided:

- Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.
- Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.
- Call **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.

## <a name="net-version-19---113"></a>.NET (version 1.9 - 1.13) 

To retrieve confirmation of customer acceptance provided previously:

Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier. Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

To retrieve confirmation of customer acceptance provided previously:

Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier. Then, get the **getAgreements** function, followed by calling the **get** function.

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

A complete sample can be found in the [GetCustomerAgreements](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

To retrieve confirmation of customer acceptance provided previously:

Use the [**Get-PartnerCustomerAgreement**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/get-partnercustomeragreement) command.

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest"></a>REST

To retrieve confirmation of customer acceptance provided previously, see the following instructions.

### <a name="rest-request"></a>REST request

Create a new **Agreement** resource with the relevant certification information.  

#### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

##### <a name="uri-parameter"></a>URI 參數

Use the following query parameter to specify the customer you are confirming.

| 名稱             | 在工作列搜尋方塊中輸入 | 必要 | 說明                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer. |

#### <a name="request-headers"></a>要求標頭

- See [Partner Center REST headers](headers.md) for more information.

#### <a name="request-body"></a>要求主體

無。

#### <a name="request-example"></a>要求的範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

### <a name="rest-response"></a>REST response

If successful, this method returns a collection of **Agreement** resources in the response body.

#### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [ 
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```

---
