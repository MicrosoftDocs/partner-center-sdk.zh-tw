---
title: 取得依搜尋欄位篩選的客戶清單
description: 取得符合篩選準則之客戶資源的集合。 您可以選擇性地設定頁面大小。 您可以依公司名稱、網域、間接轉銷商或間接雲端解決方案提供者 (CSP) 來進行篩選。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: aad9524dbe2c9edbbd7c1d50da7a448f6872fcb9
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927788"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>取得依搜尋欄位篩選的客戶清單

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得符合篩選準則之 [客戶](customer-resources.md#customer) 資源的集合。 您可以選擇性地設定頁面大小。 您可以依公司名稱、網域、間接轉銷商或間接雲端解決方案提供者 (CSP) 來進行篩選。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 使用者建造的篩選。

## <a name="c"></a>C\#

若要取得符合篩選準則的客戶集合，請先將 [**>simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) 物件具現化，以建立篩選。 您必須傳遞包含 [**>customersearchfield**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)的字串，並將篩選作業的類型指定為 [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)。 這是用戶端點所支援的唯一欄位篩選作業。 您也必須提供要用來篩選的字串。

接下來，藉由呼叫[**>buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)方法並傳遞篩選器，將[**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery)物件具現化，以傳遞至查詢。 BuildSimplyQuery 只是 [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) 類別所支援的其中一種查詢類型。

最後，若要執行篩選並取得結果，請先使用 [**>iaggregatepartner.customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) 來取得夥伴客戶作業的介面。 然後呼叫 [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) 或 [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) 方法。

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： FilterCustomers.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers？ size = {size} &filter = {FILTER} HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

使用下列查詢參數。

| 名稱   | 類型   | 必要 | 描述                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| 大小   | int    | 否       | 要一次顯示的結果數目。 這是選擇性參數。 |
| filter | filter | Yes      | 要套用到客戶的篩選條件。 這必須是編碼的字串。              |

### <a name="filter-syntax"></a>篩選語法

您必須將篩選參數撰寫成一連串逗點分隔的索引鍵/值組。 每個索引鍵和值都必須個別括住並以冒號分隔。 整個篩選條件必須加以編碼。

未編碼的範例如下所示：

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

下表描述必要的索引鍵/值組：

| Key      | 值                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| 欄位    | 要篩選的欄位。 您可以在 [**>customersearchfield**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)中找到有效的值。 |
| 值    | 篩選所依據的值。 會忽略值的大小寫。                                                                |
| 運算子 | 要套用的運算子。 此客戶案例唯一支援的值是「開頭 \_ 為」。                            |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會在回應本文中傳回符合 [客戶](customer-resources.md#customer) 資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
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
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
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
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
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
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
