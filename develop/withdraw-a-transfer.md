---
title: 收回轉移
description: 如何為客戶提取已建立的訂用帳戶轉移。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ca6804bddd4e19254d70b4bfc0626f31a087ebb0
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157820"
---
# <a name="withdraw-a-transfer"></a>收回轉移

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 現有傳輸的傳輸識別碼。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| **DELETE**| [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1。1      |

### <a name="uri-parameter"></a>URI 參數

使用下列路徑參數來識別客戶。

| 名稱            | 類型     | 必要 | 描述                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **客戶識別碼** | 字串   | 是      | 識別客戶的 GUID 格式客戶識別碼。             |
| **轉移-識別碼** | 字串   | 是      | 識別傳輸的 GUID 格式的傳輸識別碼。             |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-example"></a>要求範例

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法就不會傳回任何內容（204）。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
