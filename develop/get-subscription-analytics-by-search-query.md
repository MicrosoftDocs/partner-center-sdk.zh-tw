---
title: 透過搜尋查詢取得訂用帳戶分析
description: 如何取得搜尋查詢所篩選的訂用帳戶分析資訊。
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 4cb71638c5ad2c3a708d2eaf874fe904803cd712
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416661"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>取得搜尋查詢所篩選的訂用帳戶分析資訊

**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


如何為您的客戶取得搜尋查詢所篩選的訂用帳戶分析資訊。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用使用者認證進行驗證。


## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求語法**

| 方法 | 要求 URI |
|--------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions？ filter = {filter_string} |

 

**URI 參數**

使用下列必要的 path 參數來識別您的組織並篩選搜尋。

| 名稱 | 類型 | 必要項 | 描述 |
|------|------|----------|-------------|
| filter_string | string | 是 | 要套用至訂用帳戶分析的篩選準則。 請參閱篩選語法和篩選欄位章節，以瞭解要在此參數中使用的語法、欄位和運算子。 |
 

**篩選語法**

篩選參數必須以一系列的欄位、值和運算子組合來組成。 您可以使用**and**或**or**運算子來結合多個組合。  

未編碼的範例看起來像這樣：
- 字串：？ filter = Field 運算子 ' Value '
- Boolean：？ filter = Field 運算子值
- Contains？ filter = contains （field，' value '）


**篩選欄位**

要求的 filter 參數包含一個或多個語句，可篩選回應中的資料列。 每個陳述式包含一個與 **eq** 或 **ne** 運算子關聯的欄位和值，而某些欄位同時也支援 **contains**、**gt**、**lt**、**ge** 及 **le** 運算子。 語句可以使用**and**或**or**運算子結合。

以下是篩選字串的範例：  
 
```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```  

下表顯示篩選參數支援的欄位和支援運算子清單。 字串值必須以單引號括住。

| 參數 | 支援的運算子 | 描述 |
|-----------|---------------------|-------------|
| CustomerTenantId | eq、ne | GUID 格式的字串，可識別客戶租使用者。 |
| customerName | 包含 | 客戶的名稱。 |
| customerMarket | eq、ne | 客戶執行業務的國家/地區。 |
| id | eq、ne | 識別訂用帳戶的 GUID 格式字串。 |
| status | eq、ne | 訂用帳戶狀態。 支援的值為： "ACTIVE"、"暫止" 或 "取消布建"。 |
| productName | contains、eq、ne | 產品的名稱。 |
| subscriptionType | eq、ne | 訂閱類型。 **注意**：此欄位會區分大小寫。 支援的值為： "Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS"。 |
| autoRenewEnabled | eq、ne | 值，指出是否自動更新訂用帳戶。 |
| partnerId | eq、ne | MPN 識別碼。 若為直接轉銷商，這會是合作夥伴的 MPN 識別碼。 若為間接轉銷商，這將是間接轉銷商的 MPN 識別碼。 |
| friendlyName | 包含 | 訂閱的名稱。 |
| partnerName | string | 購買訂閱之夥伴的名稱 |  
| providerName | string | 若為間接轉銷商的訂閱交易，提供者名稱就是購買訂閱的間接提供者。
| creationDate | eq、ne、gt、lt、ge、le  | 建立訂用帳戶的日期。 |
| RateplaNcharge.effectivestartdate | eq、ne、gt、lt、ge、le | 訂用帳戶開始的日期。 |
| commitmentEndDate | eq、ne、gt、lt、ge、le  | 訂閱結束的日期。 |
| currentStateEndDate | eq、ne、gt、lt、ge、le | 訂用帳戶的目前狀態將會變更的日期。 |
| trialToPaidConversionDate | eq、ne、gt、lt、ge、le  | 訂用帳戶從試用版轉換成付費的日期。 預設值為 null。 |
| trialStartDate | eq、ne、gt、lt、ge、le | 訂用帳戶的試用期開始日期。 預設值為 null。 |
| lastUsageDate | eq、ne、gt、lt、ge、le | 上次使用訂用帳戶的日期。 預設值為 null。 |
| deprovisionedDate | eq、ne、gt、lt、ge、le | 取消布建訂用帳戶的日期。 預設值為 null。 |
| lastRenewalDate | eq、ne、gt、lt、ge、le | 上次更新訂用帳戶的日期。 預設值為 null。 |


**要求標頭** 

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

None。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 回應


如果成功，回應主體會包含符合 fileter 準則的[訂](partner-center-analytics-resources.md#subscription)用帳戶資源集合。

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
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>另請參閱

 - [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
