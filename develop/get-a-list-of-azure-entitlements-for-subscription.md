---
title: 取得訂用帳戶的 Azure 權利清單
description: 您可以使用 AzureEntitlement 資源來取得屬於訂用帳戶的 Azure 權利資源集合。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 788ad84ca128995067886f67fa70c17239cfd95a
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487498"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a>取得訂用帳戶的 Azure 權利清單

適用於：

- 合作夥伴中心

您可以使用[Azure 權利資源](subscription-resources.md#azureentitlement)（**AzureEntitlement**）來取得屬於訂用帳戶的資源集合。

## <a name="prerequisites"></a>先決條件

- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（**客戶租使用者 id**）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇客戶，選取 [**帳戶**]，然後儲存其**Microsoft ID**，以在合作夥伴中心查詢。
- 訂用帳戶識別碼。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

下表列出取得訂用帳戶的所有 Azure 權利所需的查詢參數。

| 名字                   | 類型     | 必要 | 說明                           |
|------------------------|----------|----------|---------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 對應至客戶的 GUID。 |
| **訂用帳戶識別碼**       | **guid** | Y        | 對應至訂用帳戶的 GUID。    |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求的範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回[**AzureEntitlement**](subscription-resources.md#azureentitlement)資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }