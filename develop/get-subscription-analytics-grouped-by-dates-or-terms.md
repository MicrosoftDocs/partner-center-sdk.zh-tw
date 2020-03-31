---
title: 取得依日期或詞彙分組的訂用帳戶分析
description: 如何取得依日期或詞彙分組的訂用帳戶分析資訊。
ms.assetid: 5D0C0649-F64D-40A9-ACCC-2077E2D2BA4E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: eb16bcde0b2e246f797926276eab02d6ac7a3f4f
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416642"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>取得依日期或詞彙分組的訂用帳戶分析

**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


如何取得客戶的訂用帳戶分析資訊，並依日期或詞彙分組。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。


## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求語法**

| 方法 | 要求 URI |
|--------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions？ groupby = {groupby_queries} |

 
**URI 參數**

使用下列必要的 path 參數來識別您的組織，並將結果分組。

| 名稱 | 類型 | 必要項 | 描述 |
|------|------|----------|-------------|
| groupby_queries | 字串與日期時間的配對 | 是 | 用來篩選結果的詞彙和日期。 |

 

**GroupBy 語法**

Group by 參數必須以一系列以逗號分隔的域值來組成。

未編碼的範例看起來像這樣：  

```http
?groupby=termField1,dateField1,termField2
```

下表顯示 [群組依據] 支援的欄位清單。

| 欄位 | 類型 | 描述 |
|-------|------|-------------|
| CustomerTenantId | string | GUID 格式的字串，可識別客戶租使用者。 |  
| customerName | string | 客戶的名稱。 |  
| customerMarket | string | 客戶執行業務的國家/地區。 |  
| id | string | 識別訂用帳戶的 GUID 格式字串。 |  
| status | string | 訂用帳戶狀態。 支援的值為： "ACTIVE"、"暫止" 或 "取消布建"。 |  
| productName | string | 產品的名稱。 |  
| subscriptionType | string | 訂閱類型。 注意：此欄位會區分大小寫。 支援的值為： "Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS"。 |  
| autoRenewEnabled | 布林值 | 值，指出是否自動更新訂用帳戶。 |  
| partnerId  | string | MPN 識別碼。 若為直接轉銷商，這會是合作夥伴的 MPN 識別碼。 若為間接轉銷商，這將是間接轉銷商的 MPN 識別碼。 |  
| friendlyName | string | 訂閱的名稱。 |  
| partnerName | string | 購買訂閱之夥伴的名稱 |  
| providerName | string | 若為間接轉銷商的訂閱交易，提供者名稱就是購買訂閱的間接提供者。
| creationDate | UTC 日期時間格式的字串 | 建立訂用帳戶的日期。 |  
| RateplaNcharge.effectivestartdate | UTC 日期時間格式的字串 | 訂用帳戶開始的日期。 |  
| commitmentEndDate | UTC 日期時間格式的字串 | 訂閱結束的日期。 |  
| currentStateEndDate | UTC 日期時間格式的字串 | 訂用帳戶的目前狀態將會變更的日期。 |  
| trialToPaidConversionDate | UTC 日期時間格式的字串 | 訂用帳戶從試用版轉換成付費的日期。 預設值為 null。 |  
| trialStartDate | UTC 日期時間格式的字串 | 訂用帳戶的試用期開始日期。 預設值為 null。 |  
| lastUsageDate | UTC 日期時間格式的字串 | 上次使用訂用帳戶的日期。 預設值為 null。 |  
| deprovisionedDate | UTC 日期時間格式的字串 | 取消布建訂用帳戶的日期。 預設值為 null。 |  
| lastRenewalDate | UTC 日期時間格式的字串 | 上次更新訂用帳戶的日期。 預設值為 null。 |  

**篩選欄位**

下表列出選擇性的篩選欄位和其描述：

| 欄位 | 類型 |  描述 |
|-------|------|--------------|
| 上 | int | 要在要求中傳回的資料列數目。 如果未指定此值，則最大值和預設值為10000。 如果查詢中有更多資料列，回應主體將會包含您可以用來要求下一頁資料的下一頁連結。 |
| skip | int | 在查詢中要略過的資料列數目。 使用此參數來循頁瀏覽大型資料集。 例如，top = 10000 和 skip = 0 會抓取前10000個數據列，top = 10000，skip = 10000 會抓取下一個10000個數據列。 |
| 篩選器 | string | 一或多個篩選回應中資料列的陳述式。 每個篩選語句都會包含回應主體的功能變數名稱，以及與**eq**、 **ne**或特定欄位（ **contains**運算子）相關聯的值。 陳述式可以使用 **and** 或 **or** 來結合。 在篩選參數中，字串值必須以單引號括住。 請參閱下一節，以取得可篩選的欄位清單，以及這些欄位支援的運算子。 |
| aggregationLevel | string | 指定要擷取彙總資料的時間範圍。 可以是下列其中一個字串：**day**、**week** 或 **month**。 如果未指定此值，則預設為**dateRange**。 **注意**：只有在將日期欄位當做 groupBy 參數的一部分傳遞時，此參數才適用。 |
| groupBy | string | 將資料彙總僅套用至指定欄位的陳述式。 |


**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType  
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 回應

如果成功，回應主體會包含依指定的詞彙和日期分組的[訂](partner-center-analytics-resources.md#subscription)用帳戶資源集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>另請參閱

 - [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)