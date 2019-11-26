---
title: Get subscription analytics by search query
description: How to get subscription analytics information filtered by a search query.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d742dce1d9f3cb24da4da70281ca04b0030d87b2
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487258"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Get subscription analytics information filtered by a search query

**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


How to get subscription analytics information for your customers filtered by a search query.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.


## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request


**Request syntax**

| 方法 | 要求 URI |
|--------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string} |

 

**URI parameters**

Use the following required path parameter to identify your organization and filter the search.

| 名稱 | 在工作列搜尋方塊中輸入 | 必要 | 說明 |
|------|------|----------|-------------|
| filter_string | 字串 | [是] | The filter to apply to the subscription analytics. See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter. |
 

**Filter syntax**

The filter parameter must be composed as a series of field, value and operator combinations. Multiple combinations can be combined using **and** or **or** operators.  

An unencoded example looks like this:
- String: ?filter=Field operator 'Value'
- Boolean: ?filter=Field operator Value
- Contains ?filter=contains(field,'value')


**Filter fields**

The filter parameter of the request contains one or more statements that filter the rows in the response. 每個陳述式包含一個與 **eq** 或 **ne** 運算子關聯的欄位和值，而某些欄位同時也支援 **contains**、**gt**、**lt**、**ge** 及 **le** 運算子。 Statements can be combined using **and** or **or** operators.

The following are examples of filter strings:  
 
```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```  

The following table shows a list of the supported fields and support operators for the filter parameter. String values must be surrounded by single quotes.

| 參數 | 支援的運算子 | 說明 |
|-----------|---------------------|-------------|
| customerTenantId | eq,ne | A GUID-formatted string that identifies the customer tenant. |
| customerName | contains | The name of the customer. |
| customerMarket | eq,ne | The country/region that the customer does business in. |
| id | eq,ne | A GUID-formatted string that identifies the subscription. |
| 狀態 | eq,ne | The subscription status. Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED". |
| productName | contains, eq,ne | 產品的名稱。 |
| subscriptionType | eq,ne | The subscription type. **Note**: This field is case sensitive. Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | eq,ne | A value indicating whether the subscription is renewed automatically. |
| partnerId | eq,ne | The MPN ID. For a direct reseller, this will be the MPN ID of the partner. For an indirect reseller, this will be the MPN ID of the indirect reseller. |
| friendlyName | contains | The name of the subscription. |
| partnerName | 字串 | Name of the partner for whom the subscription was purchased |  
| providerName | 字串 | When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.
| creationDate | eq、ne、gt、lt、ge、le  | The date the subscription was created. |
| effectiveStartDate | eq、ne、gt、lt、ge、le | The date the subscription starts. |
| commitmentEndDate | eq、ne、gt、lt、ge、le  | The date the subscription ends. |
| currentStateEndDate | eq、ne、gt、lt、ge、le | The date that the current status of the subscription will change. |
| trialToPaidConversionDate | eq、ne、gt、lt、ge、le  | The date that the subscription converts from trial to paid. The default value is null. |
| trialStartDate | eq、ne、gt、lt、ge、le | The date that the trial period for the subscription started. The default value is null. |
| lastUsageDate | eq、ne、gt、lt、ge、le | The date that the subscription was last used. The default value is null. |
| deprovisionedDate | eq、ne、gt、lt、ge、le | The date that the subscription was deprovisioned. The default value is null. |
| lastRenewalDate | eq、ne、gt、lt、ge、le | The date that the subscription was last renewed. The default value is null. |


**Request headers** 

- See [Headers](headers.md) for more information.

**Request body**

無。

**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response


If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription) resources that meet the fileter criteria.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

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

## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>See also

 - [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
