---
title: 刪除自助式原則
description: 如何刪除自助服務原則。
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 8c1227c6e24f0358ecfe7967e2f87b8313a33ac5
ms.sourcegitcommit: f71c7fb2fef51ac7ca0a28717d5f7276bd20ec56
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82564336"
---
# <a name="delete-a-selfservepolicy"></a>刪除 SelfServePolicy

**適用於：**

- 合作夥伴中心

本主題說明如何更新自助服務原則。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                   |
|---------|-------------------------------------------------------------------------------|
| **DELETE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1。1 |

**URI 參數**

使用下列路徑參數來取得指定的產品。

| 名稱                       | 類型         | 必要 | 描述                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-id**     | **string**   | 是      | 識別自助服務原則的字串。                 |

### <a name="request-headers"></a>要求標頭

- 需要要求識別碼和相互關聯識別碼。
- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>Request body

無。

### <a name="request-example"></a>要求範例

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a>REST 回應

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
