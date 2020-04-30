---
title: 取得發票收據對帳單
description: 使用發票識別碼和回條識別碼來抓取發票收據。
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6767337f2d3510f7ac98d61c060e2ee8c1191514
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157460"
---
# <a name="get-invoice-receipt-statement"></a>取得發票收據對帳單

**適用于**

- 合作夥伴中心

使用發票識別碼和回條識別碼來抓取發票收據。

> [!IMPORTANT]
> 這項功能僅適用于臺灣稅務收據。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 有效的發票識別碼和對應的接收識別碼。

## <a name="c"></a>C\#

若要依識別碼取得發票回條，請從合作夥伴中心 SDK v 1.12.0 開始，使用您的**ipartner.getinvoices**集合，並使用發票識別碼呼叫**ById （）** 方法，然後呼叫回條**集合並**呼叫**ById （** ），然後呼叫**Documents （）** 和**語句（）** 方法來存取發票回條語句。 最後，呼叫**Get （）** 或**GetAsync （）** 方法。

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSample**類別**： GetInvoiceReceiptStatement.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來取得發票收據語句。

| 名稱       | 類型   | 必要 | 描述                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| 發票識別碼 | 字串 | 是      | 值是發票識別碼，可讓轉銷商篩選特定發票的結果。 |
| 收據識別碼 | 字串 | 是      | 此值是可讓轉銷商篩選指定發票之收據的回條識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

None

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回 pdf 資料流程。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
