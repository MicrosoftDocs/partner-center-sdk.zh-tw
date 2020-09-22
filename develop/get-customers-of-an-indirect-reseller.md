---
title: 取得間接轉銷商的客戶
description: 如何取得間接轉銷商的客戶清單。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: caf8a4ce707624672215e5b2a0c46659e0f9564b
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927081"
---
# <a name="get-customers-of-an-indirect-reseller"></a>取得間接轉銷商的客戶

**適用於**

- 合作夥伴中心

如何取得間接轉銷商的客戶清單。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。

- 間接轉銷商的租使用者識別碼。

## <a name="c"></a>C\#

若要取得與指定間接轉銷商具有關聯性的客戶集合，請先將 [**>simplefieldfilter**/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) 物件具現化，以建立篩選。 您必須傳遞轉換成字串的 [**>customersearchfield. IndirectReseller**/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) 列舉成員，並指示 [**FieldFilterOperation. StartsWith**/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) 做為篩選作業的類型。 您也必須提供間接轉銷商的租使用者識別碼以進行篩選。

接下來，將 [**iQuery**/dotnet/api/microsoft.store.partnercenter.models.query.iquery) 物件具現化，方法是呼叫 [**>buildsimplequery**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) 方法並將篩選準則傳遞給查詢。 BuildSimplyQuery 只是 [**QueryFactory**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) 類別所支援的其中一種查詢類型。

若要執行篩選並取得結果，請先使用 [**>iaggregatepartner.customers**/dotnet/api/microsoft.store.partnercenter.ipartner.customers) ，以取得夥伴客戶作業的介面。 然後，呼叫 [**Query**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) 或 [**QueryAsync**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) 方法。

若要建立用於遍歷分頁結果的列舉值，請從 [>iaggregatepartner.customers] 的 [**IAggregatePartner.Enumerators.Customers**]/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) 屬性取得客戶集合列舉值 factory 介面，然後呼叫 [**create**/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) （如下列程式碼所示），並傳遞持有客戶集合的變數。

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

**範例**： [主控台測試應用程式](console-test-app.md)**專案**：合作夥伴中心 SDK 範例 **類別**： GetCustomersOfIndirectReseller.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers？ size = {size}？ filter = {FILTER} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來建立要求。

| 名稱   | 類型   | 必要 | 描述                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 大小   | int    | 否       | 要一次顯示的結果數目。 這是選擇性參數。                                                                                                                                                                                                                |
| filter | filter | Yes      | 篩選搜尋的查詢。 若要取得指定間接轉銷商的客戶，您必須插入間接轉銷商識別碼，並將下列字串編碼： {"Field"： "IndirectReseller"，"Value"： "{間接轉銷商識別碼}"，"Operator"： "開頭 \_ 為"}。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example-encoded"></a>要求範例 (編碼) 

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a> (解碼) 的要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含轉售商客戶的相關資訊。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
