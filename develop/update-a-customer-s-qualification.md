---
title: 更新客戶的資格
description: 更新客戶的資格，包括與設定檔相關聯的位址。
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0896c44ab193ca564ee210f48f536382c8070305
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414961"
---
# <a name="update-a-customers-qualification"></a>更新客戶的資格


**適用於**

- 夥伴中心

更新客戶的資格。

合作夥伴可以將客戶的資格更新為「教育」或「GovernmentCommunityCloud」。 無法設定其他值「None」和「非盈利性」。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

若要更新客戶對「教育」的資格，請在現有[**客戶**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer?view=partnercenter-dotnet-latest)上呼叫 **[update](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** 。

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


## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求

**要求語法**

| 方法  | 要求 URI                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification？ code = {VALIDATIONCODE} HTTP/1。1 |


**URI 參數**

使用下列查詢參數來更新限定性。

| 名稱                   | 類型 | 必要項 | 描述                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | GUID | 是      | 值是 GUID 格式的**客戶租使用者識別碼**，可讓轉銷商針對屬於轉銷商的特定客戶篩選其結果。 |
| **validationCode**     | int  | 否       | 只有政府機關雲端才需要。                                                                                                            |


**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

來自[**CustomerQualification**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)列舉的整數值。

**要求範例**

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

3
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 回應

如果成功，此方法會在回應主體中傳回更新的[**限定**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification)性屬性。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-topics"></a>相關主題

- [取得客戶資格](get-a-customer-s-qualification.md)
- [取得合作夥伴的驗證碼](get-a-partner-s-validation-codes.md)