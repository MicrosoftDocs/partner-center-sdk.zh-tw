---
title: 取得客戶接受 Microsoft Cloud 合約的確認
description: 本主題說明如何確認客戶接受 Microsoft Cloud 合約。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d6282a82793f2bc9fa6f436ed9c7a6a31ad0969d
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78899885"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>取得客戶接受 Microsoft Cloud 合約的確認

**適用于**

- 夥伴中心

> [!NOTE]  
> **合約**資源目前僅由 Microsoft 公用雲端中的合作夥伴中心支援。 不適用於：
> - 由 21Vianet 營運的合作夥伴中心
> - Microsoft Cloud 德國合作夥伴中心
> - Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="prerequisites"></a>必要條件

- 如果您使用合作夥伴中心 .NET SDK，則需要1.9 或更新版本。
- 如果您使用合作夥伴中心 JAVA SDK，則需要1.8 或更新版本。
- 如[合作夥伴中心驗證](./partner-center-authentication.md)中所述的認證。 此案例僅支援應用程式 + 使用者驗證。
- 客戶識別碼（客戶租使用者識別碼）。

## <a name="net-version-14-or-newer"></a>.NET （1.4 版或更新版本）

若要取得先前提供之客戶接受的確認：

- 使用 [ **iaggregatepartner.customers.byid** ] 集合，並使用指定的客戶識別碼來呼叫**ById**方法。
- 藉由呼叫**ByAgreementType**方法，提取 [合約 **] 屬性，並將結果**篩選為 Microsoft Cloud 協定。
- 呼叫**Get**或**GetAsync**方法。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

您可以從[主控台測試應用程式](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)專案的[GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs)類別中找到完整的範例。

## <a name="net-version-19---113"></a>.NET （版本 1.9-1.13） 

若要取得先前提供的客戶接受確認：

使用 [ **iaggregatepartner.customers.byid** ] 集合，並使用指定的客戶識別碼來呼叫**ById**方法。 然後，取得合約**屬性，** 接著呼叫**get**或**GetAsync**方法。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

若要取得先前提供的客戶接受確認：

使用**iaggregatepartner.customers.byid. getCustomers**函式，並使用指定的客戶識別碼來呼叫**byId**函數。 接著，取得**getAgreements**函式，然後呼叫**get**函式。

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

您可以從[主控台測試應用程式](https://github.com/Microsoft/Partner-Center-Java-Samples)專案的[GetCustomerAgreements](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java)類別中找到完整的範例。

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

若要取得先前提供的客戶接受確認：

使用[**PartnerCustomerAgreement**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/get-partnercustomeragreement)命令。

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest"></a>REST

若要取得先前提供的客戶接受確認，請參閱下列指示。

### <a name="rest-request"></a>REST 要求

建立具有相關認證資訊的新**協定**資源。  

#### <a name="request-syntax"></a>要求的語法

| 方法 | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1。1 |

##### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來指定您要確認的客戶。

| 名稱             | 類型 | 必要項 | 描述                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | 此值是 GUID 格式的**CustomerTenantId** ，可讓您指定客戶。 |

#### <a name="request-headers"></a>要求標頭

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

#### <a name="request-body"></a>要求本文

None。

#### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

### <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回**合約**資源的集合。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

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
