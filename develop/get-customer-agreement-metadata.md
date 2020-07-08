---
title: 取得 Microsoft 客戶合約的合約中繼資料
description: 本文說明如何取得 Microsoft 客戶合約的合約中繼資料。
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 45cc1284d872072a80a973cfee5a6218452a2409
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096962"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>取得 Microsoft 客戶合約的合約中繼資料

**適用於：**

- 合作夥伴中心

Microsoft 客戶合約的合約中繼資料目前僅由合作夥伴中心在*microsoft 公用雲端*中提供支援。 其不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您必須先取得 Microsoft 客戶合約的合約中繼資料，才能：

- [確認客戶接受 Microsoft 客戶合約](./confirm-customer-consent-customer-agreement.md)
- [取得 Microsoft 客戶合約範本的下載連結](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>必要條件

- 如果您使用合作夥伴中心 .NET SDK，則需要 1.14 版或更新版本。

- 認證，如[合作夥伴中心驗證](./partner-center-authentication.md)所述。 此案例僅支援應用程式 + 使用者驗證。

## <a name="net-version-114-or-newer"></a>.NET （1.14 版或更新版本）

若要取得 Microsoft 客戶合約的合約中繼資料：

1. 首先，取出**iaggregatepartner.customers.byid. AgreementDetails**集合。

2. 呼叫**ByAgreementType**方法，以將集合篩選為 Microsoft 客戶合約。

3. 最後，呼叫**Get**或**GetAsync**方法。

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

您可以從[主控台測試應用程式](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)專案的[GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs)類別中找到完整的範例。

## <a name="rest-request"></a>REST 要求

若要取得 Microsoft 客戶合約的合約中繼資料：

1. 建立 REST 要求以取得[AgreementMetaData](./agreement-metadata-resources.md)集合。

2. 使用**agreementType**查詢參數，將結果的範圍限定為 Microsoft 客戶合約。

### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [* \{ baseURL \} *](partner-center-rest-urls.md)/v1/agreements？ agreementType = {合約類型} HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

| 名稱                   | 類型     | 必要 | 說明                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| 合約類型 | 字串 | No | 使用此參數將查詢回應的範圍限定為特定的合約類型。 支援的值為： <ul><li>**MicrosoftCloudAgreement** ，其中只包含*MicrosoftCloudAgreement*類型的合約中繼資料</li><li>**MicrosoftCustomerAgreement** ，其中只包含*MicrosoftCustomerAgreement*類型的合約中繼資料。</li><li>**\*** 傳回所有合約中繼資料的。 （ **\*** 除非您的程式碼具有必要的執行時間邏輯來處理不熟悉的合約類型，否則請不要使用），因為 Microsoft 可能會隨時使用新的合約類型來引進合約中繼資料）。</li></ul> 如果未指定 URI 參數，則查詢會預設為**MicrosoftCloudAgreement**以提供回溯相容性。  |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回[ **AgreementMetaData**資源](./agreement-metadata-resources.md)的集合。

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
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
