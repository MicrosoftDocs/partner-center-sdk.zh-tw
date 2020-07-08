---
title: 取得授權使用資訊
description: 如何取得 Office 和 Dynamics 工作負載層級的授權使用量資訊。
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a65f007ca368cf06a2248fa716166a0b01e509da
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096781"
---
# <a name="get-licenses-usage-information"></a>取得授權使用資訊

**適用於**

- 合作夥伴中心

如何取得 Office 和 Dynamics 工作負載層級的授權使用量資訊。

## <a name="prerequisites"></a>必要條件

認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/HTTP/1。1 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="uri-parameters"></a>URI 參數

| 參數         | 類型     | 說明 | 必要 |
|-------------------|----------|-------------|----------|
| top               | 字串   | 在要求中傳回的資料列數目。 如果未指定，最大值和預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。 | No |
| skip              | int      | 在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 例如，top=10000 且 skip=0 將擷取前 10000 個資料列的資料，top=10000 且 skip=10000 將擷取下 10000 個資料列的資料，以此類推。 | No |
| filter            | 字串   | <p>要求的 <em>filter</em> 參數包含在回應中篩選資料列的一或多個陳述式。 每個語句都包含與或運算子相關聯的欄位和值 **`eq`** **`ne`** ，而且語句可以使用或結合 **`and`** **`or`** 。 下列為一些範例 <em>filter</em> 參數：</p><ul><li><em>filter = workloadCode eq ' SFB '</em></li><li><em>filter = workloadCode eq ' SFB '</em> or （<em>通道 Eq ' 轉售商 '</em>）</li></ul><p>您可以指定下欄欄位</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>頻道</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | No |
| groupby           | 字串   | <p>將資料彙總僅套用至指定欄位的陳述式。 您可以指定下列欄位：</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>頻道</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>傳回的資料列將包含 <em>groupby</em> 參數中指定的欄位，以及下列項目：</p><ul><li><strong>licensesActive</strong></li><li><strong>licensesQualified</strong></li></ul> | No |
| processedDateTime | Datetime | 其中一個可以指定處理使用量資料的日期。 預設為處理資料時的最新日期 | No |

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含下欄欄位，其中包含授權使用方式的相關資料。

| 欄位             | 類型     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | 字串   | 工作負載程式碼                                 |
| workloadName      | 字串   | 工作負載名稱                                 |
| serviceCode       | 字串   | 服務程式碼                                  |
| serviceName       | 字串   | 服務名稱                                  |
| 通道           | 字串   | 頻道名稱，轉銷商                        |
| customerTenantId  | 字串   | 客戶的唯一識別碼            |
| customerName      | 字串   | 客戶名稱                                 |
| productId         | 字串   | 產品的唯一識別碼             |
| productName       | 字串   | 產品名稱                                  |
| licensesActive    | long     | 每個工作負載的作用中授權數目        |
| licensesQualified | long     | 工作負載的合格授權數目 |
| processedDateTime | Datetime | 上次處理資料的日期         |

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
