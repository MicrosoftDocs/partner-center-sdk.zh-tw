---
title: Get all indirect resellers analytics information
description: How to get all the indirect resellers analytics information.
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
# <a name="get-all-indirect-resellers-analytics-information"></a>Get all indirect resellers analytics information

**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


How to get all the indirect resellers analytics information for your customers. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only. 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request


**Request syntax**

| 方法  | 要求 URI |
|---------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

 

**URI parameters**

<table>
<thead>
    <th>參數</th>
    <th>在工作列搜尋方塊中輸入</th>
    <th>說明</th>
</thead>
<tbody>
    <tr>
        <td>partnerTenantId</td>
        <td>字串</td>
        <td>The Tenant ID of the partner for which you want to retrieve indirect resellers data. </td>
    </tr>
    <tr>
        <td>id</td>
        <td>字串</td>
        <td>Indirect reseller ID</td>
    </tr>
    <tr>
        <td>name</td>
        <td>字串</td>
        <td>The Name of the partner for which you want to retrieve indirect resellers data.</td>
    </tr>
    <tr>
        <td>market</td>
        <td>字串</td>
        <td>The Market of the partner for which you want to retrieve indirect resellers data.</td>
    </tr>
    <tr>
        <td>firstSubscriptionCreationDate</td>
        <td>string in UTC date time format</td>
        <td>The creation date of the first subscription based on which you want to retrieve indirect resellers data.</td>
    </tr>
    <tr>
        <td>latestSubscriptionCreationDate</td>
        <td>string in UTC date time format</td>
        <td>The creation date of the latest subscription.</td>
    </tr>
    <tr>
        <td>firstSubscriptionEndDate</td>
        <td>string in UTC date time format</td>
        <td>First time any subscription was ended.</td>
    </tr>
    <tr>
        <td>latestSubscriptionEndDate</td>
        <td>string in UTC date time format</td>
        <td>Latest date when any subscription was ended. </td>
    </tr>
    <tr>
        <td>firstSubscriptionSuspendedDate</td>
        <td>string in UTC date time format</td>
        <td>First time any subscription was suspended.</td>
    </tr>
    <tr>
        <td>latestSubscriptionSuspendedDate</td>
        <td>string in UTC date time format</td>
        <td>Latest date when any subscription was suspended.</td>
    </tr>
    <tr>
        <td>firstSubscriptionDeprovisionedDate</td>
        <td>string in UTC date time format</td>
        <td>First time any subscription was deprovisioned.</td>
    </tr>
    <tr>
        <td>latestSubscriptionDeprovisionedDate</td>
        <td>string in UTC date time format</td>
        <td>Latest date when any subscription was deprovisioned.</td>
    </tr>
    <tr>
        <td>subscriptionCount</td>
        <td>double</td>
        <td>Subscription count for all value added resellers</td>
    </tr>
    <tr>
        <td>licenseCount</td>
        <td>double</td>
        <td>License count for all value added resellers</td>
    </tr>
    <tr>
        <td>indirectResellerCount</td>
        <td>double</td>
        <td>Indirect resellers count</td>
    </tr>
    <tr>
        <td>top</td>
        <td>字串</td>
        <td>在要求中傳回的資料列數目。 如果未指定，最大值和預設值為 10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。</td>
    </tr>
    <tr>
        <td>skip</td>
        <td>整數</td>
        <td>
          <p>在查詢中要略過的資料列數目。 使用此參數來瀏覽大型資料集。 For example, <code>top=10000 and skip=0</code> retrieves the first 10000 rows of data, <code>top=10000 and skip=10000</code> retrieves the next 10000 rows of data, and so on.</p>
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
                <li><em>market</em></li>
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
        <td><p>指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：&quot;day&quot;、&quot;week&quot; 或 &quot;month&quot;。 如果沒有指定，則預設為 &quot;天&quot;。</p>
        <p><em>aggregationLevel</em> is not supported without a <strong>groupby</strong>. <em>aggregationLevel</em> applies to all <strong>datefields</strong> present in the <strong>groupby</strong></p>
        </td>
    </tr>
    <tr>
        <td>orderby</td>
        <td>字串</td>
        <td>
            <p>對每個安裝的結果資料值做出排序的陳述式。 The syntax is <code>...&orderby=field[order],field [order],...</code> The field parameter can be one of the following strings:</p>
            <ul>
                <li>&quot;partnerTenantId&quot;</li> 
                <li>&quot;id&quot;</li> 
                <li>&quot;name&quot;</li> 
                <li>&quot;market&quot;</li> 
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
                <li><em>id</em></li>
                <li><em>名稱</em></li>
                <li><em>market</em></li>
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
 

**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

無。

**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, the response body contains a collection of [indirect resellers](partner-center-analytics-resources.md#indirect_resellers) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>See also
 - [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
