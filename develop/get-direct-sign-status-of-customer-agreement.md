---
title: 取得客戶對 Microsoft 客戶合約的直接簽署狀態。
description: 您可以使用 DirectSignedCustomerAgreementStatus 資源來取得 Microsoft 客戶合約之客戶直接簽署（直接接受）的狀態。
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0d07630a23ad4d18f992f2fcd9db2d19c637df98
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415946"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>取得 Microsoft 客戶合約的客戶直接簽署（直接接受）的狀態

適用於：

- 夥伴中心

合作夥伴中心目前僅支援在 Microsoft 公用雲端中使用**DirectSignedCustomerAgreementStatus**資源。

此資源不適*用於：*

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本文會說明如何取得客戶直接接受 Microsoft 客戶合約的狀態。

## <a name="rest-request"></a>REST 要求

若要取得客戶直接接受 Microsoft 客戶合約的狀態，請建立 REST 要求來取得客戶的[DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) 。 

### <a name="request-syntax"></a>要求的語法

使用下列要求語法：

| 方法 | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

您可以搭配您的要求使用下列 URI 參數：

| 名稱             | 類型 | 必要項 | 描述                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | 是 | 此值是 GUID 格式的**CustomerTenantId** ，可讓您指定客戶的租使用者識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

None。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回[ **DirectSignedCustomerAgreementStatus**資源](./customer-agreement-direct-sign-status-resource.md)。

資源具有**isSigned**屬性，可指出客戶的直接簽署（直接接受）狀態。 

- 值為**true**表示合約已直接由客戶簽署（接受）。
- 值為**false**時，表示*合約尚未直接*由客戶簽署（接受）。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 

請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```