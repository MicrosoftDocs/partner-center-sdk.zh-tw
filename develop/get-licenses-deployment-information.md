---
title: Get licenses deployment information
description: How to get deployment information for Office and Dynamics licenses.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: c5a9808e350cd67488153bf8271223f95d984682
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488598"
---
# <a name="get-licenses-deployment-information"></a>Get licenses deployment information

**Applies To**

- 合作夥伴中心

How to get deployment information for Office and Dynamics licenses.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.


## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>Request

**Request syntax**

| 方法  | 要求 URI                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

 
**Request headers**

- See [Partner Center REST headers](headers.md) for more information.  

**URI parameters**

| 參數         | 在工作列搜尋方塊中輸入     | 說明 | 必要 |  
|-------------------|----------|-------------|----------|  
| top               | 字串   | 在要求中傳回的資料列數目。 如果未指定，最大值和預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。 | 無 | 
| skip              | 整數      | 在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 例如，top=10000 且 skip=0 將擷取前 10000 個資料列的資料，top=10000 且 skip=10000 將擷取下 10000 個資料列的資料，以此類推。 | 無 | 
| filter            | 字串   | <p>要求的 <em>filter</em> 參數包含在回應中篩選資料列的一或多個陳述式。 每個陳述式包含一個與 **eq** 或 **ne** 運算子關聯的欄位和值，而陳述式可以使用 **and** 或 **or** 結合。 下列為一些範例 <em>filter</em> 參數：</p><ul><li><em>filter=serviceCode eq 'O365'</em></li><li><em>filter=serviceCode eq 'O365'</em> or (<em>channel eq 'Reseller'</em>)</li></ul><p>You can specify the following fields</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | 無 | 
| groupby           | 字串   | <p>將資料彙總僅套用至指定欄位的陳述式。 您可以指定下列欄位：</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>傳回的資料列將包含 <em>groupby</em> 參數中指定的欄位，以及下列項目：</p><ul><li><strong>licensesDeployed</strong></li><li><strong>licensesSold</strong></li></ul> | 無 | 
| processedDateTime | DateTime | One can specify the date from which usage data was processed. Defaults to the latest date when the data was processed | 無 | 


**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```


## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>Response

If successful, the response body contains the following fields containing data about the licenses deployed.

| 欄位             | 在工作列搜尋方塊中輸入     | 說明                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | 字串   | Service code                          |
| serviceName       | 字串   | 服務名稱                          |
| channel           | 字串   | Channel name, reseller                |
| customerTenantId  | 字串   | Unique identifier for the customer    |
| customerName      | 字串   | [客戶名稱]                         |
| productId         | 字串   | Unique identifier for the product     |
| productName       | 字串   | [產品名稱]                          |
| licensesDeployed  | 長整數     | Number of licenses deployed           |
| licensesSold      | 長整數     | 售出的授權數目               |
| processedDateTime | DateTime | Date when the data was last processed |



**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

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