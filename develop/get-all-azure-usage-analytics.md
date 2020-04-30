---
title: 取得所有 Azure 使用情形的分析資訊
description: 如何取得所有 Azure 使用量分析資訊。
ms.assetid: CDBD04A4-BA34-49B8-9815-7C19253E6C70
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e05ab42b154457ae0db079ff0d90d836a7da7d3e
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156760"
---
# <a name="get-all-azure-usage-analytics-information"></a>取得所有 Azure 使用情形的分析資訊

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何取得客戶的所有 Azure 使用量分析資訊。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI |
|---------|-------------|
| **GET** | baseURL/partner/v1/analytics/usage/azure HTTP/1.1 [* \{ \} *](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>URI 參數

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
        <p>在要求中傳回的資料列數目。 如果未指定，最大值和預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>skip</p>
      </td>
      <td>
        <p>int</p>
      </td>
      <td>
        <p>在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 例如， <code>top=10000 and skip=0</code>會抓取前10000個數據列， <code>top=10000 and skip=10000</code>並抓取接下來的10000個數據列，依此類推。</p>
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
        <p>要求的 <em>filter</em> 參數包含在回應中篩選資料列的一或多個陳述式。 每個語句都包含與<strong> <code>eq</code> </strong> <strong> <code>ne</code> </strong>或運算子相關聯的欄位和值，而且語句可以使用<strong> <code>and</code> </strong>或<strong> <code>or</code> </strong>結合。 您可以指定下列各項：</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
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
        <p>指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串： <code>day</code>、 <code>week</code>或。 <code>month</code> 如果未指定，則預設<code>day</code>值為。</p>
      <p>在<code>aggregationLevel</code>沒有的<code>groupby</code>情況下，不支援參數。 <code>aggregationLevel</code>參數會套用至存在於中的<code>groupby</code>所有日期欄位。</p>
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
        <p>對每個安裝的結果資料值做出排序的陳述式。 語法為 <code>...&orderby=field [order],field [order],...</code>。 <code>field</code>參數可以是下列其中一個字串：</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p><em>Order</em>參數是選擇性的，而且可以<code>asc</code>是<code>desc</code>或;分別指定每個欄位的遞增或遞減順序。 預設值為 <code>asc</code>。</p>
        <p><strong>範例：</strong><br/>
          <code>...&orderby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>groupby</code></p>
      </td>
      <td>
        <p>字串</p>
      </td>
      <td>
        <p>將資料彙總僅套用至指定欄位的陳述式。 您可以指定下列欄位：</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p>傳回的資料列將包含<code>groupby</code>參數中所指定的欄位，以及<em>數量</em>。</p>
        <p><code>groupby</code>參數可以與<code>aggregationLevel</code>參數搭配使用。</p>
        <p><strong>範例：</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[Azure 使用量](partner-center-analytics-resources.md#csp-program-azure-usage-analytics)資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

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

## <a name="see-also"></a>另請參閱

- [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
