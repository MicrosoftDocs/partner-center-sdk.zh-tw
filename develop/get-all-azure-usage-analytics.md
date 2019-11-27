---
title: 取得所有 Azure 使用量分析資訊
description: 如何取得所有 Azure 使用量分析資訊。
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
# <a name="get-all-azure-usage-analytics-information"></a>取得所有 Azure 使用量分析資訊

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


如何取得客戶的所有 Azure 使用量分析資訊。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例僅支援使用使用者認證進行驗證。 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求語法**

| 方法  | 要求 URI |
|---------|-------------|
| **獲取** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1。1 |

 

**URI 參數**

<table>
  <thead>
      <th>
        <p>參數</p>
      </th>
      <th>
        <p>類型</p>
      </th>
      <th>
        <p>描述</p>
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
        <p>要在要求中傳回的資料列數目。 最大值及未指定的預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。</p>
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
        <p>在查詢中要略過的資料列數目。 使用此參數來循頁瀏覽大型資料集。 例如，<code>top=10000 and skip=0</code> 會抓取前10000個數據列，<code>top=10000 and skip=10000</code> 抓取後續10000個數據列，依此類推。</p>
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
          <li><em>訂閱</em></li>
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
        <p>指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：&quot;day&quot;、&quot;week&quot; 或 &quot;month&quot;。 如果沒有指定，則預設為 &quot;day&quot;。</p>
      <p>如果沒有<em>groupby</em>，就不支援<em>aggregationLevel</em>參數。 <em>AggregationLevel</em>參數會套用到出現在<em>groupby</em>中的所有日期欄位。</p>
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
        <p>對每個安裝的結果資料值做出排序的陳述式。 語法是 <code>...&orderby=field [order],field [order],...</code><em>欄位</em>參數可以是下列其中一個字串：</p>
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
        <p><em>Order</em>參數是選擇性的，可以 &quot;asc&quot; 或 &quot;desc&quot; 分別指定每個欄位的遞增或遞減順序。 預設為 &quot;asc&quot;。</p>
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
          <li><em>訂閱</em></li>
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
        <p>傳回的資料列將包含<em>groupby</em>參數中指定的欄位，以及<em>數量</em>。</p>
        <p><em>groupby</em> 參數可以搭配 <em>aggregationLevel</em> 參數使用。</p>
        <p><strong>範例：</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>


**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

無。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應主體會包含[Azure 使用量](partner-center-analytics-resources.md#azure_usage)資源的集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>另請參閱
  - [合作夥伴中心分析-資源](partner-center-analytics-resources.md)

