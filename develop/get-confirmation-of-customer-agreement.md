---
title: 取得客戶對 Microsoft 客戶合約的接受確認
description: 本主題說明如何確認客戶接受 Microsoft 客戶合約。
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 4cf76af611d05913f04d8c9268d61acf16334d76
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416013"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>取得客戶對 Microsoft 客戶合約的接受確認

適用於：

- 夥伴中心

**合約**資源目前僅由合作夥伴中心在*Microsoft 公用雲端*中受到支援。 此資源不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

這篇文章說明如何取得客戶接受 Microsoft 客戶合約的確認。

## <a name="prerequisites"></a>必要條件

- 如果您使用合作夥伴中心 .NET SDK，則需要 1.14 版或更新版本。
- 認證，如[合作夥伴中心驗證](./partner-center-authentication.md)所述。 此案例僅支援應用程式 + 使用者驗證。
- 客戶識別碼 (**customer-tenant-id**)。

## <a name="net"></a>.NET

若要取得先前提供之客戶接受的確認：

- 使用 [ **iaggregatepartner.customers.byid** ] 集合，並使用指定的客戶識別碼來呼叫**ById**方法。
- 藉由呼叫**ByAgreementType**方法，提取 [合約 **] 屬性，並將結果**篩選為 Microsoft 客戶合約。
- 呼叫**Get**或**GetAsync**方法。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

您可以從[主控台測試應用程式](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)專案的[GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs)類別中找到完整的範例。


## <a name="rest-request"></a>REST 要求

若要取得先前提供之客戶接受的確認：

1. 建立 REST 要求，以取得客戶的[合約集合。](./agreement-resources.md) 
2. 使用**agreementType**查詢參數將結果的範圍限定為 Microsoft 客戶合約。

### <a name="request-syntax"></a>要求的語法

使用下列要求語法：

| 方法 | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/V1/customers/{customer-tenant-id}/agreements？ agreementType = {合約類型} HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

您可以搭配您的要求使用下列 URI 參數：

| 名稱             | 類型 | 必要項 | 描述                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | 是 | 此值是 GUID 格式的**CustomerTenantId** ，可讓您指定客戶。 |
| 合約類型 | string | 否 | 此參數會傳回所有合約中繼資料。 使用此參數將查詢回應的範圍限定為特定的合約類型。 支援的值為： <ul><li>僅包含*MicrosoftCloudAgreement*類型之協定中繼資料的**MicrosoftCloudAgreement** 。</li><li>僅包含*MicrosoftCustomerAgreement*類型之協定中繼資料的**MicrosoftCustomerAgreement** 。</li><li>傳回所有合約中繼資料的 **\*** 。 （除非您的程式碼具有處理非預期協定類型所需的邏輯，否則請不要使用 **\*** ）。</li></ul> 如果未指定 URI 參數，則查詢會預設為**MicrosoftCloudAgreement**以提供回溯相容性。 Microsoft 可能會隨時以新的合約類型引進合約中繼資料。  |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

None。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**合約**資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 

請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

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
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
