---
title: 確認客戶接受 Microsoft 客戶合約
description: 確認客戶接受 Microsoft 客戶合約。
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
# <a name="confirm-customer-acceptance-of-microsoft-customer-agreement"></a>確認客戶接受 Microsoft 客戶合約

適用於：

- 合作夥伴中心

合作夥伴中心目前僅支援在*microsoft 公用雲端*中確認客戶接受 Microsoft 客戶合約。 此功能目前不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本文說明如何確認或重新確認客戶接受 Microsoft 客戶合約。

## <a name="prerequisites"></a>必要條件

- 如果您使用合作夥伴中心 .NET SDK，則需要1.14 或更新版本。
- 如[合作夥伴中心驗證](./partner-center-authentication.md)中所述的認證。 *此案例僅支援應用程式 + 使用者驗證。*
- 客戶識別碼（**客戶租使用者 id**）。
- 當客戶接受 Microsoft 客戶合約時的日期（**dateAgreed**）。
- 來自已接受 Microsoft 客戶合約之客戶組織使用者的相關資訊。 這包括：
  - 名字
  - 姓氏
  - 電子郵件地址
  - 電話號碼 (選用)

## <a name="net"></a>.NET

若要確認或重新確認客戶接受 Microsoft 客戶合約：

1. 取得 Microsoft 客戶合約的合約中繼資料。 您必須取得 Microsoft 客戶合約的**templateId** 。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](get-customer-agreement-metadata.md)。

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. 建立包含確認詳細資料的新**協定**物件。
3. 使用**IAgreggatePartner**集合，並使用指定的**客戶租使用者識別碼**來呼叫**ById**方法。
4. 使用 [**協定**] 屬性，然後呼叫**Create**或**CreateAsync**。

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

您可以從[主控台測試應用程式](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)專案的[CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs)類別中找到完整的範例。


## <a name="rest-request"></a>REST 要求

若要確認或重新確認客戶接受 Microsoft 客戶合約：

1. 取得 Microsoft 客戶合約的合約中繼資料。 您必須取得 Microsoft 客戶合約的**templateId** 。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](get-customer-agreement-metadata.md)。
2. 建立新的[**合約**資源](agreement-resources.md)，以確認客戶已接受 Microsoft 客戶合約。 使用下列[REST 要求語法](#request-syntax)。

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來指定您要確認的客戶。

| 名稱               | 類型 | 必要 | 描述                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| 客戶-租使用者識別碼 | GUID | 是 | 值是 GUID 格式的**客戶租使用者**識別碼，這是可讓您指定客戶的識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述 REST 要求主體中的必要屬性。

| 名稱      | 類型   | 描述                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| 合約 | 物件 | 合作夥伴提供的詳細資料，以確認客戶接受 Microsoft 客戶合約。 |  

#### <a name="agreement"></a>合約

下表描述用來建立[**合約**資源](agreement-resources.md)的最小必要欄位。

| 屬性       | 類型   | 描述                              |
|----------------|--------|------------------------------------------|
| primaryContact | [連絡人](./utility-resources.md#contact) | 來自已接受 Microsoft Cloud 合約之客戶組織使用者的相關資訊，包括： **firstName**、 **lastName**、 **email**和**phoneNumber** （選擇性） |
| dateAgreed     | UTC 日期時間格式的字串 |客戶接受合約的日期。 |
| templateId     | 字串 | 客戶接受之合約類型的唯一識別碼。 您可以藉由抓取 Microsoft 客戶合約的合約中繼資料，取得 Microsoft 客戶合約的**templateId** 。 如需詳細資訊，請參閱[取得 Microsoft Cloud 合約的合約中繼資料](./get-customer-agreement-metadata.md)。 |
| type           | 字串 | 客戶接受的合約類型。 如果客戶接受 Microsoft 客戶合約，請使用 "MicrosoftCustomerAgreement"。 |
  
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

### <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回[**協定**資源](./agreement-resources.md)。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 

使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

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
