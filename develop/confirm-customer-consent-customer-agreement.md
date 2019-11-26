---
title: Confirm customer acceptance of Microsoft Customer Agreement
description: Confirm customer acceptance of the Microsoft Customer Agreement.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7c7c3acea0f2e45b53fde7372bbb1f33fcb9de13
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488948"
---
# <a name="confirm-customer-acceptance-of-microsoft-customer-agreement"></a>Confirm customer acceptance of Microsoft Customer Agreement

適用於：

- 合作夥伴中心

Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*. This functionality doesn't currently apply to:

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.

## <a name="prerequisites"></a>必要條件

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). *This scenario only supports App+User authentication.*
- A customer identifier (**customer-tenant-id**).
- The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.
- Information about the user from the customer organization that accepted the Microsoft Customer Agreement. 這包括：
  - 名字
  - 姓氏
  - Email address
  - 電話號碼 (選用)

## <a name="net"></a>.NET

To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Create a new **Agreement** object containing details of the confirmation.
3. Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.
4. Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.

```csharp
// string selectedCustomerId;

var agreementToCreate = new Agreement
{
    DateAgreed = DateTime.UtcNow,
    TemplateId = microsoftCustomerAgreementDetails.TemplateId,
    PrimaryContact = new Contact
    {
        FirstName = "Tania",
        LastName = "Carr",
        Email = "someone@example.com",
        PhoneNumber = "1234567890"
    }
};

Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
```

A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.


## <a name="rest-request"></a>REST request

To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).
2. Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement. Use the following [REST request syntax](#request-syntax).

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI 參數

Use the following query parameter to specify the customer that you're confirming.

| 名稱               | 在工作列搜尋方塊中輸入 | 必要 | 說明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | [是] | The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer. |

### <a name="request-headers"></a>要求標頭

For more information, see [Partner Center REST headers](headers.md).

### <a name="request-body"></a>要求主體

This table describes the required properties in the REST request body.

| 名稱      | 在工作列搜尋方塊中輸入   | 說明                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| 合約 | 物件 | Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement. |  

#### <a name="agreement"></a>合約

This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).

| 屬性       | 在工作列搜尋方塊中輸入   | 說明                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Contact](./utility-resources.md#contact) | Information about the user from the customer organization who accepted the Microsoft Cloud Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional) |
| dateAgreed     | string in UTC date time format |The date when the customer accepted the agreement. |
| templateId     | 字串 | Unique identifier of the agreement type accepted by the customer. You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. See [Get agreement metadata for Microsoft Cloud Agreement](./get-customer-agreement-metadata.md) for details. |
| type           | 字串 | Agreement type accepted by the customer. Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement. |
  
#### <a name="request-example"></a>要求的範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

### <a name="rest-response"></a>REST Response

If successful, this method returns an [**Agreement** resource](./agreement-resources.md).

#### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. 

Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
