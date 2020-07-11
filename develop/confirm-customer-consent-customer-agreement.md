---
title: 確認客戶接受 Microsoft 客戶合約
description: 確認客戶接受 Microsoft 客戶合約。
ms.date: 02/04/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66ffa499594816fdcaa86ed805bb64c252663e4d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096396"
---
# <a name="confirm-customer-acceptance-of-microsoft-customer-agreement"></a>確認客戶接受 Microsoft 客戶合約

**適用於：**

- 合作夥伴中心

合作夥伴中心目前僅支援在「Microsoft 公用雲端」  中確認客戶是否接受 Microsoft 客戶合約。 此功能目前不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本文將說明如何確認或重新確認客戶是否接受 Microsoft 客戶合約。

## <a name="prerequisites"></a>必要條件

- 如果您使用合作夥伴中心 .NET SDK，則需要 1.14 版或更新版本。

- 認證，如[合作夥伴中心驗證](./partner-center-authentication.md)所述。 此案例僅支援「應用程式 + 使用者」驗證。 

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 客戶接受 Microsoft 客戶合約時的日期 (**dateAgreed**)。

- 客戶組織中已接受 Microsoft 客戶合約的使用者相關資訊。 這包括：
  - 名字
  - 姓氏
  - 電子郵件地址
  - 電話號碼 (選用)

## <a name="net"></a>.NET

若要確認或重新確認客戶是否接受 Microsoft 客戶合約：

1. 擷取 Microsoft 客戶合約的合約中繼資料。 您必須取得 Microsoft 客戶合約的 **templateId**。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](get-customer-agreement-metadata.md)。

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. 建立包含確認詳細資料的新**合約**物件。

3. 使用 **IAgreggatePartner.Customers** 集合，並使用指定的 **customer-tenant-id**來呼叫 **ById** 方法。

4. 使用 **Agreements** 屬性，然後呼叫 **Create** 或 **CreateAsync**。

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

您可以從[主控台測試應用程式](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)專案的 [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) 類別中找到完整範例。

## <a name="rest-request"></a>REST 要求

若要確認或重新確認客戶是否接受 Microsoft 客戶合約：

1. 擷取 Microsoft 客戶合約的合約中繼資料。 您必須取得 Microsoft 客戶合約的 **templateId**。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](get-customer-agreement-metadata.md)。

2. 建立新的[**合約**資源](agreement-resources.md)，確認客戶已接受 Microsoft 客戶合約。 請使用下列 [REST 要求語法](#request-syntax)。

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來指定您要確認的客戶。

| 名稱               | 類型 | 必要 | 說明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | 是 | 此值是 GUID 格式的 **customer-tenant-id**，此識別碼可讓您用來指定客戶。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表說明 REST 要求主體中的必要屬性。

| 名稱      | 類型   | 說明                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| 合約 | 物件 | 合作夥伴提供的詳細資料，用來確認客戶是否接受 Microsoft 客戶合約。 |

#### <a name="agreement"></a>合約

下表說明用來建立[**合約**資源](agreement-resources.md)的最低必要欄位數目。

| 屬性       | 類型   | 說明                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Contact](./utility-resources.md#contact) | 客戶組織中已接受 Microsoft 客戶合約的使用者相關資訊，包括：**firstName**、**lastName**、**email** 和 **phoneNumber** (選擇性) |
| dateAgreed     | UTC 日期時間格式的字串 |客戶接受合約的日期。 |
| templateId     | 字串 | 客戶所接受合約類型的唯一識別碼。 您可以藉由擷取 Microsoft 客戶合約的合約中繼資料，取得 Microsoft 客戶合約的 **templateId**。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](./get-customer-agreement-metadata.md)。 |
| 型別           | 字串 | 客戶接受的合約類型。 如果客戶已接受 Microsoft 客戶合約，請使用 "MicrosoftCustomerAgreement"。 |

#### <a name="request-example"></a>要求範例

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

## <a name="rest-response"></a>REST 回應

如果成功，此方法會傳回[**合約**資源](./agreement-resources.md)。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。

請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

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
