---
title: 取得授權部署資訊
description: 如何取得 Office 和 Dynamics 授權的部署資訊。
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ad91b8082315e5c35ae43e70b44b94f5a948938b
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415756"
---
# <a name="get-licenses-deployment-information"></a>取得授權部署資訊

**適用於**

- 夥伴中心

如何取得 Office 和 Dynamics 授權的部署資訊。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。


## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求

**要求語法**

| 方法  | 要求 URI                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/HTTP/1。1 |

 
**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。  

**URI 參數**

| 參數         | 類型     | 描述 | 必要項 |  
|-------------------|----------|-------------|----------|  
| 上               | string   | 要在要求中傳回的資料列數目。 最大值及未指定的預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。 | 否 | 
| skip              | int      | 在查詢中要略過的資料列數目。 使用此參數來循頁瀏覽大型資料集。 例如，top=10000 且 skip=0 將擷取前 10000 個資料列的資料，top=10000 且 skip=10000 將擷取下 10000 個資料列的資料，以此類推。 | 否 | 
| 篩選器            | string   | <p>要求的 <em>filter</em> 參數包含在回應中篩選資料列的一或多個陳述式。 每個陳述式包含一個與 **eq** 或 **ne** 運算子關聯的欄位和值，而陳述式可以使用 **and** 或 **or** 結合。 下列為一些範例 <em>filter</em> 參數：</p><ul><li><em>filter = serviceCode eq ' O365 '</em></li><li><em>篩選 = serviceCode eq ' O365 '</em>或（<em>通道 Eq ' 轉售商 '</em>）</li></ul><p>您可以指定下欄欄位</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>頻道</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | 否 | 
| groupby           | string   | <p>將資料彙總僅套用至指定欄位的陳述式。 您可以指定下列欄位：</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>頻道</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>傳回的資料列將包含 <em>groupby</em> 參數中指定的欄位，以及下列項目：</p><ul><li><strong>licensesDeployed</strong></li><li><strong>licensesSold</strong></li></ul> | 否 | 
| processedDateTime | DateTime | 其中一個可以指定處理使用量資料的日期。 預設為處理資料時的最新日期 | 否 | 


**要求範例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```


## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應

如果成功，回應主體會包含下欄欄位，其中包含已部署之授權的相關資料。

| 欄位             | 類型     | 描述                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | string   | 服務程式代碼                          |
| serviceName       | string   | 服務名稱                          |
| 頻道           | string   | 頻道名稱，轉銷商                |
| CustomerTenantId  | string   | 客戶的唯一識別碼    |
| customerName      | string   | 客戶名稱                         |
| productId         | string   | 產品的唯一識別碼     |
| productName       | string   | 產品名稱                          |
| licensesDeployed  | long     | 已部署的授權數目           |
| licensesSold      | long     | 售出的授權數目               |
| processedDateTime | DateTime | 上次處理資料的日期 |



**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```