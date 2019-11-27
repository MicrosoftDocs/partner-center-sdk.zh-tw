---
title: 取得所有間接轉售商分析資訊
description: 如何取得所有間接轉銷商分析資訊。
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a13814e2e53d89e326b436bba4e134ba41c72547
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485978"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>取得所有間接轉售商分析資訊

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


如何取得客戶的所有間接轉銷商分析資訊。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例僅支援使用使用者認證進行驗證。 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求語法**

| 方法  | 要求 URI |
|---------|-------------|
| **獲取** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1。1 |

 

**URI 參數**

<table>
<thead>
    <th>參數</th>
    <th>類型</th>
    <th>描述</th>
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
        <td>name</td>
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
        <td>要在要求中傳回的資料列數目。 最大值及未指定的預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。</td>
    </tr>
    <tr>
        <td>skip</td>
        <td>整數</td>
        <td>
          <p>在查詢中要略過的資料列數目。 使用此參數來循頁瀏覽大型資料集。 例如，<code>top=10000 and skip=0</code> 會抓取前10000個數據列，<code>top=10000 and skip=10000</code> 抓取後續10000個數據列，依此類推。</p>
        </td>
    </tr>
    <tr>
        <td>filter</td>
        <td>字串</td>
        <td>
            <p>要求的 <em>filter</em> 參數包含在回應中篩選資料列的一或多個陳述式。 每個陳述式包含一個與 <strong>eq</strong> 或 <strong>ne</strong> 運算子關聯的欄位和值，而陳述式可以使用 <strong>and</strong> 或 <strong>or</strong> 結合。 您可以指定下列欄位：</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>號</em></li>
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
            <p><strong>範例：</strong></br>
              <code>.../indirectresellers?filter=market eq &#39;US&#39;</code></p>
            <p><strong>範例：</strong></br>
                <code>.../indirectresellers?filter=market eq &#39;US&#39; or (firstSubscriptionCreationDate le cast(&#39;2018-01-01&#39;,Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast(&#39;2018-04-01&#39;,Edm.DateTimeOffset))</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>aggregationLevel</td>
        <td>字串</td>
        <td><p>指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：&quot;day&quot;、&quot;week&quot; 或 &quot;month&quot;。 如果沒有指定，則預設為 &quot;day&quot;。</p>
        <p>不支援<strong>groupby</strong>的<em>aggregationLevel</em> 。 <em>aggregationLevel</em>適用于所有出現在<strong>groupby</strong>中的<strong>datefields</strong></p>
        </td>
    </tr>
    <tr>
        <td>orderby</td>
        <td>字串</td>
        <td>
            <p>對每個安裝的結果資料值做出排序的陳述式。 語法是 <code>...&orderby=field[order],field [order],...</code> 欄位參數可以是下列其中一個字串：</p>
            <ul>
                <li>&quot;partnerTenantId&quot;</li> 
                <li>&quot;識別碼&quot;</li> 
                <li>&quot;name&quot;</li> 
                <li>&quot;市場&quot;</li> 
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
            <p><em>order</em> 參數為選擇性，並可以是 &quot;asc&quot; 或 &quot;desc&quot;，以指定每個欄位的遞增或遞減順序。 預設為 &quot;asc&quot;。</p>
            <p><strong>範例：</strong></br> 
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
                <li><em>號</em></li>
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
            <p>傳回的資料列將包含 <em>groupby</em> 參數中指定的欄位，以及下列項目：</p>
            <ul>
                <li><em>indirectResellerCount</em></li>
                <li><em>licenseCount</em></li>
                <li><em>subscriptionCount</em></li>
            </ul>
            <p><em>groupby</em> 參數可以搭配 <em>aggregationLevel</em> 參數使用。</p>
            <p><strong>範例：</strong></br>
                <code>...&groupby=ageGroup,market&aggregationLevel=week</code>
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
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應主體會包含[間接轉售商](partner-center-analytics-resources.md#indirect_resellers)資源的集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>另請參閱
 - [合作夥伴中心分析-資源](partner-center-analytics-resources.md)
