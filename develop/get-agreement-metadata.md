---
title: 取得 Microsoft Cloud 合約的合約中繼資料
description: 本主題說明如何取得 Microsoft Cloud 合約的合約中繼資料。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0608a735705e02fe70ceabfd60d33cda6a9e4d0e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486098"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>取得 Microsoft Cloud 合約的合約中繼資料

**適用于**

- 合作夥伴中心

> [!NOTE]  
> **AgreementMetaData**資源目前僅由 Microsoft 公用雲端中的合作夥伴中心支援。 不適用於：
> - 由 21Vianet 營運的合作夥伴中心
> - Microsoft Cloud 德國合作夥伴中心
> - Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="prerequisites"></a>必要條件

- 如果您使用合作夥伴中心 .NET SDK，則需要1.9 或更新版本。
- 如果您使用合作夥伴中心 JAVA SDK，則需要1.8 或更新版本。
- 如[合作夥伴中心驗證](./partner-center-authentication.md)中所述的認證。 此案例支援應用程式 + 使用者驗證。

## <a name="net-version-114-or-newer"></a>.NET （1.14 版或更新版本）

若要取得 Microsoft Cloud 合約的合約中繼資料：

1. 首先，取出**iaggregatepartner.customers.byid. AgreementDetails**集合。

2. 呼叫**ByAgreementType**方法，以 Microsoft Cloud 協定來篩選集合。

3. 最後，呼叫**Get**或**GetAsync**方法。

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

您可以從[主控台測試應用程式](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)專案的[GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs)類別中找到完整的範例。

## <a name="net-version-19---113"></a>.NET （版本 1.9-1.13）

若要取得 Microsoft Cloud 合約的合約中繼資料：

先取出**iaggregatepartner.customers.byid. AgreementDetails**集合，然後呼叫**Get**或**GetAsync**方法。 然後在集合內搜尋與 Microsoft Cloud 合約對應的專案：

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

若要取得 Microsoft Cloud 合約的合約中繼資料：

先呼叫**iaggregatepartner.customers.byid. getAgreementDetails**函式，然後呼叫**get**函式。 然後在集合內搜尋與 Microsoft Cloud 合約對應的專案：

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

您可以從[主控台測試應用程式](https://github.com/Microsoft/Partner-Center-Java-Samples)專案的[GetAgreementDetails](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java)類別中找到完整的範例。

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

若要取得 Microsoft Cloud 合約的合約中繼資料：

使用[**PartnerAgreementDetail**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/get-partneragreementdetail)命令。 然後在集合內搜尋與 Microsoft Cloud 合約對應的專案：

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest"></a>停

### <a name="rest-request"></a>REST 要求

若要取得 Microsoft Cloud 合約的合約中繼資料，請先建立 REST 要求來取得**AgreementMetaData**集合。 然後在集合中搜尋對應至 Microsoft Cloud 協定的專案。

#### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/agreements HTTP/1。1 |

#### <a name="request-headers"></a>要求標頭

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

#### <a name="request-body"></a>要求本文

無。

#### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

### <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**AgreementMetaData**資源的集合。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

#### <a name="response-example"></a>回應範例

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

若要識別回應中對應至 Microsoft Cloud 合約的資源，請尋找**agreementType**屬性值為 "MicrosoftCloudAgreement" 的資源。

---
