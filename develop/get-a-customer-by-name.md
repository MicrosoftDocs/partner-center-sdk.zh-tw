---
title: 取得依搜尋欄位篩選的客戶清單
description: 取得符合篩選準則的客戶資源集合。 您可以選擇性地設定頁面大小。 您可以依公司名稱、網域、間接轉銷商或間接雲端解決方案提供者（CSP）進行篩選。
ms.assetid: 7D5D8C83-1DBD-4C54-8CDA-FE0CAC911D14
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f99a91139a1341dcd82efe3727a9603beb3f1622
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413355"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>取得依搜尋欄位篩選的客戶清單


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

取得符合篩選準則的[客戶](customer-resources.md#customer)資源集合。 您可以選擇性地設定頁面大小。 您可以依公司名稱、網域、間接轉銷商或間接雲端解決方案提供者（CSP）進行篩選。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 使用者結構化的篩選準則。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取得符合篩選準則的客戶集合，請先將[**SimpleFieldFilter**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter)物件具現化，以建立篩選準則。 您必須傳遞包含[**CustomerSearchField**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)的字串，並將篩選作業的類型指定為[**FieldFilterOperation. StartsWith**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)。 這是用戶端點唯一支援的欄位篩選作業。 您也必須提供要用來篩選的字串。

接下來，藉由呼叫[**BuildSimpleQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)方法並將篩選準則傳遞給查詢，將[**iQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.iquery)物件具現化。 BuildSimplyQuery 只是[**QueryFactory**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)類別支援的其中一個查詢類型。

最後，若要執行篩選並取得結果，請先使用[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers)來取得合作夥伴客戶作業的介面。 然後呼叫[**Query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query)或[**QueryAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)方法。

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

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： FilterCustomers.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求


**要求語法**

| 方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers？ size = {size} & 篩選準則 = {FILTER} HTTP/1。1 |

 

**URI 參數**

使用下列查詢參數。

| 名稱   | 類型   | 必要項 | 描述                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | int    | 否       | 要一次顯示的結果數目。 這個參數是選擇性的。 |
| 篩選器 | 篩選器 | 是      | 要套用至客戶的篩選準則。 這必須是已編碼的字串。              |

 

**篩選語法**

您必須以一系列以逗號分隔的索引鍵/值組來撰寫篩選參數。 每個索引鍵和值都必須個別加上引號，並以冒號分隔。 整個篩選準則必須經過編碼。

未編碼的範例看起來像這樣：

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```  
  
下表描述必要的機碼值組：

| Key      | 值                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| 欄位    | 要篩選的欄位。 可以在[**CustomerSearchField**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)中找到有效的值。 |
| 值    | 要做為篩選依據的值。 會忽略值的大小寫。                                                                |
| 運算子 | 要套用的運算子。 此客戶案例唯一支援的值是「開始\_」。                            |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

None。

**要求範例**

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

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 回應


如果成功，此方法會在回應本文中傳回相符[客戶](customer-resources.md#customer)資源的集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

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

 

 




