---
title: 啟用商業市集產品的沙箱訂用帳戶
description: 啟用商業 marketplace 產品的沙箱訂閱。
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cee833f110c45e8f53a47aed3d8a8c3b1ccd6946
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154370"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-products"></a>啟用商業市集產品的沙箱訂用帳戶

**適用於：**

- 合作夥伴中心

如何從整合沙箱帳戶啟用商業 marketplace 軟體即服務（SaaS）產品的訂閱以進行計費。

> [!NOTE]
> 您只可以從整合沙箱帳戶啟用商業 marketplace SaaS 產品的訂閱。 如果您有生產訂用帳戶，則必須造訪發行者的網站，才能完成安裝程式。 只有在安裝完成後，訂用帳戶才會開始計費。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 整合沙箱合作夥伴帳戶，其客戶具有商業 marketplace SaaS 產品的有效訂閱。

- 針對使用合作夥伴中心 .NET SDK 的合作夥伴，您必須使用 SDK version 1.14.0 或更高版本來存取這項功能。

## <a name="c"></a>C\#

使用下列步驟來啟用商業 marketplace SaaS 產品的訂用帳戶：

1. 對可用的訂用帳戶作業提供介面。 您必須識別客戶，並指定試用訂用帳戶的訂用帳戶識別碼。

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. 使用**啟用**作業來啟動訂用帳戶。

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

| 名稱                   | 類型     | 必要 | 描述                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y | 此值是 GUID 格式的客戶租使用者識別碼（**客戶租使用者 id**），可讓您指定客戶。 |
| **訂用帳戶識別碼** | **guid** | Y | 此值是 GUID 格式的訂用帳戶識別碼（訂用帳戶**id**），可讓您指定訂用帳戶。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>REST 回應

這個方法會傳回**訂**用帳戶識別碼和**狀態**屬性。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
