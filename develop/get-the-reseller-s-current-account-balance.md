---
title: 取得合作夥伴的目前帳戶餘額
description: 抓取合作夥伴目前的帳戶餘額。 週期性和一次性費用的發票餘額和總費用的摘要。
ms.assetid: 130C8230-6284-4B1F-8741-CA92E1ECA30F
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c28d4cbdb4c6a74ca983a727d72ded5cd93ecabc
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157170"
---
# <a name="get-the-partners-current-account-balance"></a>取得合作夥伴的目前帳戶餘額

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

抓取合作夥伴目前的帳戶餘額。 週期性和一次性費用的發票餘額和總費用的摘要。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

## <a name="c"></a>C\#

若要取得帳戶餘額，請使用您的**Iaggregatepartner.customers.byid 發票**集合，然後呼叫 [**摘要**] 屬性。 然後呼叫**Get**函式，最後呼叫**BalanceAmount**屬性。

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSample**類別**： GetInvoiceSummary.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                              |
|---------|--------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1。1  |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

None

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應中傳回[InvoiceSummary](invoice-resources.md#invoicesummary)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "balanceAmount": 751094.39,
    "currencyCode": "USD",
    "currencySymbol": "$",
    "accountingDate": "2018-03-16T00:00:00",
    "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
    "lastPaymentDate": "2017-01-01T12:00:00Z",
    "lastPaymentAmount": 1000,
    "latestInvoiceDate": "2018-03-16T00:00:00",
    "details": [
        {
            "invoiceType": "Recurring",
            "summary": {
                "balanceAmount": 202955.87,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "accountingDate": "2017-02-27T00:00:00Z",
                "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
                "lastPaymentDate": "2017-01-01T12:00:00Z",
                "lastPaymentAmount": 1000,
                "latestInvoiceDate": "0001-01-01T00:00:00",
                "attributes": {
                    "objectType": "InvoiceSummary"
                }
            }
        },
        {
            "invoiceType": "OneTime",
            "summary": {
                "balanceAmount": 548138.52,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "accountingDate": "2018-03-16T00:00:00",
                "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                "lastPaymentDate": "0001-01-01T00:00:00",
                "lastPaymentAmount": 0,
                "latestInvoiceDate": "2018-03-16T00:00:00",
                "attributes": {
                    "objectType": "InvoiceSummary"
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/summary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "InvoiceSummary"
    }
}
```
