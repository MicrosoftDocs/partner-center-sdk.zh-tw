---
title: 取得合作夥伴中心活動的記錄
description: 如何取得合作夥伴使用者或應用程式在一段時間內所執行作業的記錄。
ms.assetid: C24054DA-3E31-4BCD-BEB5-085564C20C58
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ef53290570d3e1c4eb8c8db0418c8b0080d80151
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490248"
---
# <a name="get-a-record-of-partner-center-activity"></a>取得合作夥伴中心活動的記錄


**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何取得合作夥伴使用者或應用程式在一段時間內所執行作業的記錄。

使用此 API，從目前的日期，或在包含開始日期和/或結束日期的指定日期範圍內，抓取過去30天的審核記錄。 不過，請注意，基於效能的考慮，活動記錄資料可用性受限於前90天。 開始日期超過目前日期之前90天的要求將會收到不正確的要求例外狀況（錯誤碼：400）和適當的訊息。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取得合作夥伴中心作業的記錄，請先建立您要取得之記錄的日期範圍。 接下來的程式碼範例只會採用開始日期，但您也可以包含結束日期。 如需詳細資訊，請參閱[**Query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query)方法。 接下來，針對您想要套用的篩選器類型建立所需的變數，並指派適當的值。 例如，若要依公司名稱 substring 進行篩選，請建立一個變數來保存子字串。 若要依客戶識別碼進行篩選，請建立一個變數來保存識別碼。

在下列範例中，會提供範例程式碼，依據公司名稱 substring、客戶識別碼或資源類型進行篩選。 選擇其中一個，並將其他專案批註。 在每個案例中，您會先使用[**其預設的**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor)函式來建立篩選器，以具現化[**SimpleFieldFilter**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter)物件。 您必須傳遞包含要搜尋之欄位的字串，以及要套用的適當運算子，如下所示。 您也必須提供要用來篩選的字串。

接下來，使用[**AuditRecords**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords)屬性來取得用來審核記錄作業的介面，並呼叫[**Query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query)或[**QueryAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync)方法來執行篩選，並取得代表結果第一頁的[**AuditRecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord)集合。 您必須將開始日期、此處範例中未使用的選擇性結束日期，以及代表實體查詢的[**IQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.iquery)物件傳遞給方法。 IQuery 物件的建立方式是將上方建立的篩選準則傳遞至[**QueryFactory 的**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)方法。

一旦有了專案的初始頁面，請使用[**AuditRecords**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)方法來建立可用於逐一查看其餘頁面的列舉值。

``` csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (e.g. "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1"; 
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource. 
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }
     
    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**資料夾**：審核

## <a name="span-idrequestspan-idrequestspan-idrequest-rest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/> REST 要求


**要求語法**

| 方法  | 要求 URI                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/auditrecords？開始日期 = {起始時間} HTTP/1。1                                                                                                     |
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/auditrecords？開始時間 = {開始時間} & 結束日期 = {結束時間} HTTP/1。1                                                                                   |
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/V1/auditrecords？起始日期 = {開始時間} & 結束時間 = {結束時間} & 篩選準則 = {"Field"： ""，"Value"： "{searchSubstring}"，"Operator"： "substring"} HTTP/1。1 |
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/V1/auditrecords？起始日期 = {開始時間} & 結束時間 = {結束時間} & 篩選準則 = {"Field"： "CustomerId"，"Value"： "{CustomerId}"，"Operator"： "equals"} HTTP/1。1          |
| **獲取** | [ *{baseURL}* ](partner-center-rest-urls.md)/V1/auditrecords？起始日期 = {開始時間} & 結束時間 = {結束時間} & 篩選準則 = {"Field"： "ResourceType"，"Value"： "{ResourceType}"，"Operator"： "equals"} HTTP/1。1      |

 

**URI 參數**

建立要求時，請使用下列查詢參數。

| 名稱      | 類型   | 必要 | 描述                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startDate | date   | 否       | 以 yyyy-mm-dd 格式的開始日期。 如果未提供任何值，結果集會預設為要求日期前的30天。 當提供篩選準則時，這個參數是選擇性的。                                          |
| endDate   | date   | 否       | 以 yyyy-mm-dd 格式的結束日期。 當提供篩選準則時，這個參數是選擇性的。 當結束日期省略或設為 null 時，要求會傳回最大的視窗，或使用今天做為結束日期，以較少者為准。 |
| filter    | 字串 | 否       | 要套用的篩選準則。 這必須是已編碼的字串。 當提供開始日期或結束日期時，這個參數是選擇性的。                                                                                              |

 

**篩選語法**您必須以一系列以逗號分隔的索引鍵/值組來撰寫篩選參數。 每個索引鍵和值都必須個別加上引號，並以冒號分隔。 整個篩選準則必須經過編碼。

未編碼的範例看起來像這樣：

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

下表描述必要的機碼值組：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>索引鍵</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>欄位</td>
<td>要篩選的欄位。 支援的值可在<a href="#request">要求語法</a>中找到。</td>
</tr>
<tr class="even">
<td>值</td>
<td>要做為篩選依據的值。 會忽略值的大小寫。 以下是支援的值參數，如<a href="#request">要求語法</a>所示：
<ul>
<li><p>searchSubstring-以公司名稱取代。 您可以輸入子字串來符合公司名稱的一部分（例如，&quot;bri&quot; 會符合 &quot;Fabrikam，Inc.&quot;）。</p>
<p>範例： &quot;值&quot;：&quot;bri&quot;</p></li>
<li><p>customerId-取代為代表客戶識別碼的 GUID 格式字串。</p>
<p>範例： &quot;值&quot;：&quot;0c39d6d5-c70d-4c55-bc02-f620844f3fd1&quot;</p></li>
<li><p>resourceType-取代為要取得其審核記錄的資源類型（例如訂用帳戶）。 可用的資源類型定義于<a href="https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype"><strong>ResourceType</strong></a>中。</p>
<p>範例： &quot;值&quot;：&quot;訂用帳戶&quot;</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>運算子</td>
<td>要套用的運算子。 您可以在<a href="#request">要求語法</a>中找到支援的運算子。</td>
</tr>
</tbody>
</table>

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴 CENTER REST 標頭](headers.md)。

**要求本文**

無。

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 回應


如果成功，這個方法會傳回符合篩選準則的一組活動。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




