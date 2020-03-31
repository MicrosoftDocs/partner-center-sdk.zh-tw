---
title: 取得合作夥伴的政府群雲端驗證碼
description: 如何取得合作夥伴的政府群雲端驗證碼。
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ea547798e591731bba2ec23ab3c125d00e758887
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412564"
---
# <a name="get-a-partners-validation-codes"></a>取得合作夥伴的驗證碼

**適用於**

- 夥伴中心

如何取得合作夥伴的政府社區雲端驗證代碼的集合。 必須有驗證碼，才能在政府機關雲端中建立客戶。

如果您想要讓組織或客戶組織核准適用于 CSP 的 Office 365 政府 GCC，請參閱[適用于 csp 的 office 365 政府 Gcc 合作夥伴和客戶資格準則](https://docs.microsoft.com/partner-center/csp-gcc-validate)。  


## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 在[此](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner)填寫表單之後確認驗證。
- 沒有資格的客戶。


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

若要取得合作夥伴的所有驗證碼清單，請呼叫**GetValidationCodes**。

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```


## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求

**要求語法**

| 方法  | 要求 URI                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1。1 |


**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```


## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應

如果成功，這個方法會傳迴響應主體中的[**ValidationCode**](utility-resources.md#validationcode)資源清單。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
