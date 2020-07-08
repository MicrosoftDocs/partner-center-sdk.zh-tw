---
title: 取得所有間接轉銷商的分析資訊
description: 如何取得所有間接轉銷商分析資訊。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 65bbc79ff456022c399a0a0c08e4561f0c7babcd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097865"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>取得所有間接轉銷商的分析資訊

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何取得客戶的所有間接轉銷商分析資訊。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI |
|---------|-------------|
| **GET** | [* \{ BASEURL \} *](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

<table>
<thead>
    <th>參數</th>
    <th>類型</th>
    <th>Description</th>
</thead>
<tbody>
    <tr>
        <td>partnerTenantId</td>
        <td>字串</td>
        <td>您要為其取得間接轉銷商資料之夥伴的租使用者識別碼。 </td>
    </tr>
    <tr>
        <td>id</td>
        <td>字串</td>
        <td>間接轉銷商識別碼</td>
    </tr>
    <tr>
        <td>NAME</td>
        <td>字串</td>
        <td>您要為其取得間接轉銷商資料的夥伴名稱。</td>
    </tr>
    <tr>
        <td>market</td>
        <td>字串</td>
        <td>您想要為其取得間接轉銷商資料的合作夥伴市場。</td>
    </tr>
    <tr>
        <td>firstSubscriptionCreationDate</td>
        <td>UTC 日期時間格式的字串</td>
        <td>您要用來抓取間接轉銷商資料的第一個訂用帳戶建立日期。</td>
    </tr>
    <tr>
        <td>latestSubscriptionCreationDate</td>
        <td>UTC 日期時間格式的字串</td>
        <td>最新訂用帳戶的建立日期。</td>
    </tr>
    <tr>
        <td>firstSubscriptionEndDate</td>
        <td>UTC 日期時間格式的字串</td>
        <td>第一次結束任何訂用帳戶。</td>
    </tr>
    <tr>
        <td>latestSubscriptionEndDate</td>
        <td>UTC 日期時間格式的字串</td>
        <td>任何訂閱結束時的最新日期。 </td>
    </tr>
    <tr>
        <td>firstSubscriptionSuspendedDate</td>
        <td>UTC 日期時間格式的字串</td>
        <td>第一次暫停任何訂用帳戶。</td>
    </tr>
    <tr>
        <td>latestSubscriptionSuspendedDate</td>
        <td>UTC 日期時間格式的字串</td>
        <td>任何訂用帳戶暫止的最新日期。</td>
    </tr>
    <tr>
        <td>firstSubscriptionDeprovisionedDate</td>
        <td>UTC 日期時間格式的字串</td>
        <td>第一次取消布建任何訂用帳戶。</td>
    </tr>
    <tr>
        <td>latestSubscriptionDeprovisionedDate</td>
        <td>UTC 日期時間格式的字串</td>
        <td>取消布建任何訂用帳戶的最新日期。</td>
    </tr>
    <tr>
        <td>subscriptionCount</td>
        <td>double</td>
        <td>所有增值轉銷商的訂用帳戶計數</td>
    </tr>
    <tr>
        <td>licenseCount</td>
        <td>double</td>
        <td>所有增值轉銷商的授權計數</td>
    </tr>
    <tr>
        <td>indirectResellerCount</td>
        <td>double</td>
        <td>間接轉銷商計數</td>
    </tr>
    <tr>
        <td>top</td>
        <td>字串</td>
        <td>在要求中傳回的資料列數目。 如果未指定，最大值和預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。</td>
    </tr>
    <tr>
        <td>skip</td>
        <td>int</td>
        <td>
          <p>在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 例如，會抓取 <code>top=10000 and skip=0</code> 前10000個數據列， <code>top=10000 and skip=10000</code> 並抓取接下來的10000個數據列，依此類推。</p>
        </td>
    </tr>
    <tr>
        <td>filter</td>
        <td>字串</td>
        <td>
            <p>要求的 <em>filter</em> 參數包含在回應中篩選資料列的一或多個陳述式。 每個陳述式包含一個與 <strong>eq</strong> 或 <strong>ne</strong> 運算子關聯的欄位和值，而陳述式可以使用 <strong>and</strong> 或 <strong>or</strong> 結合。 您可以指定下列欄位：</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>id</em></li>
                <li><em>名稱</em></li>
                <li><em>細分</em></li>
                <li><em>firstSubscriptionCreationDate</em></li>
                <li><em>latestSubscriptionCreationDate</em></li>
                <li><em>firstSubscriptionEndDate</em></li>
                <li><em>latestSubscriptionEndDate</em></li>
                <li><em>firstSubscriptionSuspendedDate</em></li>
                <li><em>latestSubscriptionSuspendedDate</em></li>
                <li><em>firstSubscriptionDeprovisionedDate</em></li>
                <li><em>latestSubscriptionDeprovisionedDate</em></li>
            </ul>
            <p><strong>範例︰</strong></br>
              <code>.../indirectresellers?filter=market eq &#39;US&#39;</code></p>
            <p><strong>範例︰</strong></br>
                <code>.../indirectresellers?filter=market eq &#39;US&#39; or (firstSubscriptionCreationDate le cast(&#39;2018-01-01&#39;,Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast(&#39;2018-04-01&#39;,Edm.DateTimeOffset))</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>aggregationLevel</td>
        <td>字串</td>
        <td><p>指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：&quot;day&quot;、&quot;week&quot; 或 &quot;month&quot;。 如果沒有指定，則預設為 &quot;天&quot;。</p>
        <p><code>aggregationLevel</code>不支援，沒有 <code>aggregationLevel</code> 。 <code>aggregationLevel</code>適用于出現在中的所有<strong>datefields</strong><code>aggregationLevel</code></p>
        </td>
    </tr>
    <tr>
        <td>orderby</td>
        <td>字串</td>
        <td>
            <p>對每個安裝的結果資料值做出排序的陳述式。 語法為 <code>...&orderby=field[order],field [order],...</code>。 field 參數可以是下列其中一個字串：</p>
            <ul>
                <li>&quot;partnerTenantId&quot;</li>
                <li>&quot;id&quot;</li>
                <li>&quot;name&quot;</li>
                <li>&quot;細分&quot;</li>
                <li>&quot;firstSubscriptionCreationDate&quot;</li>
                <li>&quot;latestSubscriptionCreationDate&quot;</li>
                <li>&quot;firstSubscriptionEndDate&quot;</li>
                <li>&quot;latestSubscriptionEndDate&quot;</li>
                <li>&quot;firstSubscriptionSuspendedDate&quot;</li>
                <li>&quot;latestSubscriptionSuspendedDate&quot;</li>
                <li>&quot;firstSubscriptionDeprovisionedDate&quot;</li>
                <li>&quot;latestSubscriptionDeprovisionedDate&quot;</li>
                <li>&quot;subscriptionCount&quot;</li>
                <li>&quot;licenseCount&quot;</li>
            </ul>
            <p><em>Order</em>參數是選擇性的，而且可以是 <code>asc</code> 或 <code>desc</code> ; 指定每個欄位的遞增或遞減順序。 預設值為 <code>asc</code>。</p>
            <p><strong>範例︰</strong></br>
                <code>...&orderby=market,subscriptionCount</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>groupby</td>
        <td>字串</td>
        <td>
            <p>將資料彙總僅套用至指定欄位的陳述式。 您可以指定下列欄位：</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>id</em></li>
                <li><em>名稱</em></li>
                <li><em>細分</em></li>
                <li><em>firstSubscriptionCreationDate</em></li>
                <li><em>latestSubscriptionCreationDate</em></li>
                <li><em>firstSubscriptionEndDate</em></li>
                <li><em>latestSubscriptionEndDate</em></li>
                <li><em>firstSubscriptionSuspendedDate</em></li>
                <li><em>latestSubscriptionSuspendedDate</em></li>
                <li><em>firstSubscriptionDeprovisionedDate</em></li>
                <li><em>latestSubscriptionDeprovisionedDate</em></li>
            </ul>
            <p>傳回的資料列包含子句中指定的欄位 <code>groupby</code> ，以及下欄欄位：</p>
            <ul>
                <li><em>indirectResellerCount</em></li>
                <li><em>licenseCount</em></li>
                <li><em>subscriptionCount</em></li>
            </ul>
            <p><code>groupby</code>參數可以與參數搭配使用 <code>aggregationLevel</code> 。</p>
            <p><strong>範例︰</strong></br>
                <code>...&groupby=ageGroup,market&aggregationLevel=week</code>
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
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[間接轉售商](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics)資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## <a name="see-also"></a>另請參閱

- [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
