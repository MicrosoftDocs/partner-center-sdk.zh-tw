---
title: 取得授權使用量資訊
description: 如何取得 Office 和 Dynamics 工作負載層級的授權使用量資訊。
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2f3d5a73ef91a8c85515addfa1c6192886a216d8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488578"
---
# <a name="get-licenses-usage-information"></a>取得授權使用量資訊

**適用于**

- 合作夥伴中心

如何取得 Office 和 Dynamics 工作負載層級的授權使用量資訊。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用應用程式 + 使用者認證進行驗證。


## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求

**要求語法**

| 方法  | 要求 URI                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/HTTP/1。1 |

 
**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**URI 參數**

| 參數         | 類型     | 描述 | 必要 |  
|-------------------|----------|-------------|----------|  
| top               | 字串   | 要在要求中傳回的資料列數目。 最大值及未指定的預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。 | 否 | 
| skip              | 整數      | 在查詢中要略過的資料列數目。 使用此參數來循頁瀏覽大型資料集。 例如，top=10000 且 skip=0 將擷取前 10000 個資料列的資料，top=10000 且 skip=10000 將擷取下 10000 個資料列的資料，以此類推。 | 否 | 
| filter            | 字串   | <p>要求的 <em>filter</em> 參數包含在回應中篩選資料列的一或多個陳述式。 每個陳述式包含一個與 **eq** 或 **ne** 運算子關聯的欄位和值，而陳述式可以使用 **and** 或 **or** 結合。 下列為一些範例 <em>filter</em> 參數：</p><ul><li><em>filter = workloadCode eq ' SFB '</em></li><li><em>filter = workloadCode eq ' SFB '</em> or （<em>通道 Eq ' 轉售商 '</em>）</li></ul><p>您可以指定下欄欄位</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>頻道</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | 否 | 
| groupby           | 字串   | <p>將資料彙總僅套用至指定欄位的陳述式。 您可以指定下列欄位：</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>頻道</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>傳回的資料列將包含 <em>groupby</em> 參數中指定的欄位，以及下列項目：</p><ul><li><strong>licensesActive</strong></li><li><strong>licensesQualified</strong></li></ul> | 否 | 
| processedDateTime | DateTime | 其中一個可以指定處理使用量資料的日期。 預設為處理資料時的最新日期 | 否 | 


**要求範例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應

如果成功，回應主體會包含下欄欄位，其中包含授權使用方式的相關資料。

| 欄位             | 類型     | 描述                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | 字串   | 工作負載程式碼                                 |
| workloadName      | 字串   | 工作負載名稱                                 |
| serviceCode       | 字串   | 服務程式代碼                                  |
| serviceName       | 字串   | 服務名稱                                  |
| 頻道           | 字串   | 頻道名稱，轉銷商                        |
| customerTenantId  | 字串   | 客戶的唯一識別碼            |
| customerName      | 字串   | [客戶名稱]                                 |
| productId         | 字串   | 產品的唯一識別碼             |
| productName       | 字串   | 產品名稱                                  |
| licensesActive    | 長整數     | 每個工作負載的作用中授權數目        |
| licensesQualified | 長整數     | 工作負載的合格授權數目 |
| processedDateTime | DateTime | 上次處理資料的日期         |


**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

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