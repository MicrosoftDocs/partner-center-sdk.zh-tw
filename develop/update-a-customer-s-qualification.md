---
title: 更新客戶的資格
description: 更新客戶的資格，包括與設定檔相關聯的位址。
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9d1bf9c7b21b0ba48ef026918b7b0694752c2eb0
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157970"
---
# <a name="update-a-customers-qualification"></a>更新客戶的資格

**適用于**

- 合作夥伴中心

更新客戶的資格。

合作夥伴可以將客戶的資格更新為「教育」或「GovernmentCommunityCloud」。 無法設定其他值「None」和「非盈利性」。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

## <a name="c"></a>C\#

若要更新客戶對「教育」的資格，請在現有[**客戶**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer?view=partnercenter-dotnet-latest)上呼叫**[update](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** 。

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSamples**類別**： CustomerQualificationOperations.cs

若要更新客戶對現有客戶**GovernmentCommunityCloud**的資格，而不限定資格。  合作夥伴也必須包含客戶的[**ValidationCode**](utility-resources.md#validationcode)。

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **提出** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification？ code = {VALIDATIONCODE} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來更新限定性。

| 名稱                   | 類型 | 必要 | 描述                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | GUID | 是      | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。 |
| **validationCode**     | int  | 否       | 只有政府機關雲端才需要。                                                                                                            |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

來自[**CustomerQualification**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)列舉的整數值。

### <a name="request-example"></a>要求範例

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回更新的[**限定**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification)性屬性。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a>相關文章

- [取得客戶資格](get-a-customer-s-qualification.md)
- [取得合作夥伴的驗證碼](get-a-partner-s-validation-codes.md)
