---
title: Get all Azure usage analytics information
description: How to get all the Azure usage analytics information.
ms.assetid: CDBD04A4-BA34-49B8-9815-7C19253E6C70
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 49df0ac0741ed486ab34015b409eced7fde59afd
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485998"
---
# <a name="get-all-azure-usage-analytics-information"></a>Get all Azure usage analytics information

**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


How to get all the Azure usage analytics information for your customers. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only. 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request


**Request syntax**

| 方法  | 要求 URI |
|---------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

 

**URI parameters**

<table>
  <thead>
      <th>
        <p>參數</p>
      </th>
      <th>
        <p>在工作列搜尋方塊中輸入</p>
      </th>
      <th>
        <p>說明</p>
      </th>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>top</p>
      </td>
      <td>
        <p>字串</p>
      </td>
      <td>
        <p>在要求中傳回的資料列數目。 如果未指定，最大值和預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>skip</p>
      </td>
      <td>
        <p>整數</p>
      </td>
      <td>
        <p>在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 For example, <code>top=10000 and skip=0</code> retrieves the first 10000 rows of data, <code>top=10000 and skip=10000</code> retrieves the next 10000 rows of data, and so on.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>filter</p>
      </td>
      <td>
        <p>字串</p>
      </td>
      <td>
        <p>要求的 <em>filter</em> 參數包含在回應中篩選資料列的一或多個陳述式。 每個陳述式包含一個與 <strong>eq</strong> 或 <strong>ne</strong> 運算子關聯的欄位和值，而陳述式可以使用 <strong>and</strong> 或 <strong>or</strong> 結合。 您可以指定下列欄位：</p>
        <ul>
          <li><em>customerTenantId</em></li>
          <li><em>customerName</em></li>
          <li><em>subscriptionId</em></li>
          <li><em>subscriptionName</em></li>
          <li><em>usageDate</em></li>
          <li><em>resourceLocation</em></li>
          <li><em>meterCategory</em></li>
          <li><em>meterSubcategory</em></li>
          <li><em>meterUnit</em></li>
          <li><em>reservationOrderId</em></li>
          <li><em>reservationId</em></li>
          <li><em>consumptionMeterId</em></li>
          <li><em>serviceType</em></li>
        </ul>
        <p><strong>範例：</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39;</code>
        </p>
        <p><strong>範例：</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39; or (usageDate le cast(&#39;2018-01-01&#39;, Edm.DateTimeOffset) and usageDate le cast(&#39;2018-04-01&#39;, Edm.DateTimeOffset))</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>aggregationLevel</p>
      </td>
      <td>
        <p>字串</p>
      </td>
      <td>
        <p>指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：&quot;day&quot;、&quot;week&quot; 或 &quot;month&quot;。 如果沒有指定，則預設為 &quot;天&quot;。</p>
      <p>The <em>aggregationLevel</em> parameter is not supported without a <em>groupby</em>. The <em>aggregationLevel</em> parameter applies to all date fields present in the <em>groupby</em>.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>orderby</p>
      </td>
      <td>
        <p>字串</p>
      </td>
      <td>
        <p>對每個安裝的結果資料值做出排序的陳述式。 The syntax is <code>...&orderby=field [order],field [order],...</code> The <em>field</em> parameter can be one of the following strings:</p>
        <ul>
          <li>&quot;customerTenantId&quot;</li>
          <li>&quot;customerName&quot;</li>
          <li>&quot;subscriptionId&quot;</li>
          <li>&quot;subscriptionName&quot;</li>
          <li>&quot;usageDate&quot;</li>
          <li>&quot;resourceLocation&quot;</li>
          <li>&quot;meterCategory&quot;</li>
          <li>&quot;meterSubcategory&quot;</li>
          <li>&quot;meterUnit&quot;</li>
          <li>&quot;reservationOrderId&quot;</li>
          <li>&quot;reservationId&quot;</li>
          <li>&quot;consumptionMeterId&quot;</li>
          <li>&quot;serviceType&quot;</li>
        </ul>
        <p>The <em>order</em> parameter is optional and can be &quot;asc&quot; or &quot;desc&quot; to specify ascending or descending order for each field, respectively. 預設為 &quot;asc&quot;。</p>
        <p><strong>範例：</strong><br/> 
          <code>...&orderby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>groupby</p>
      </td>
      <td>
        <p>字串</p>
      </td>
      <td>
        <p>將資料彙總僅套用至指定欄位的陳述式。 您可以指定下列欄位：</p>
        <ul>
          <li><em>customerTenantId</em></li>
          <li><em>customerName</em></li>
          <li><em>subscriptionId</em></li>
          <li><em>subscriptionName</em></li>
          <li><em>usageDate</em></li>
          <li><em>resourceLocation</em></li>
          <li><em>meterCategory</em></li>
          <li><em>meterSubcategory</em></li>
          <li><em>meterUnit</em></li>
          <li><em>reservationOrderId</em></li>
          <li><em>reservationId</em></li>
          <li><em>consumptionMeterId</em></li>
          <li><em>serviceType</em></li>
        </ul>
        <p>The returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the <em>Quantity</em>.</p>
        <p><em>groupby</em> 參數可以搭配 <em>aggregationLevel</em> 參數使用。</p>
        <p><strong>範例：</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>


**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

無。

**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#azure_usage) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20  
}
```


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>See also
  - [Partner Center Analytics - Resources](partner-center-analytics-resources.md)

