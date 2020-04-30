---
title: 依合作夥伴 MPN 識別碼取得客戶的訂用帳戶
description: 如何取得給定合作夥伴提供給指定客戶的訂閱清單。
ms.assetid: 02742789-97F0-4B9C-9948-42BF6F3D4D18
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 2346ebec68b56e7449a7f70fc1bf34aaf8265c3a
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156360"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a>依合作夥伴 MPN 識別碼取得客戶的訂用帳戶

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何取得給定合作夥伴提供給指定客戶的訂閱清單。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 合作夥伴 Microsoft 合作夥伴網路（MPN）識別碼。

## <a name="c"></a>C\#

若要取得給定合作夥伴提供給指定客戶的訂用帳戶清單，請先使用[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法搭配客戶識別碼來識別客戶。 然後從[**訂閱**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)屬性取得客戶訂用帳戶集合作業的介面，並使用 MPN 識別碼呼叫[**ByPartner**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner)方法，以識別夥伴並抓取夥伴訂用帳戶作業的介面。 最後，呼叫[**get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync)方法以取得集合。

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： GetSubscriptionsByMpnid.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

若要取得給定合作夥伴提供給指定客戶的訂用帳戶清單，請先使用**iaggregatepartner.customers.byid. getCustomers. byId**函數搭配客戶識別碼來識別客戶。 然後從**getSubscriptions**函式取得客戶訂用帳戶集合作業的介面，並使用 MPN ID 呼叫**byPartner**函式，以識別合作夥伴並取得合作夥伴訂用帳戶作業的介面。 最後，呼叫**get**函式以取得集合。

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

若要取得給定合作夥伴提供給指定客戶的訂用帳戶清單，請執行[**PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md)命令。 使用**CustomerId**參數指定客戶識別碼來識別客戶，並在**MpnId**參數中填入 MPN 識別碼，以識別合作夥伴。

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI |
|---------|----------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions？ mpn\_id = {MPN-id} HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

使用下列路徑和查詢參數來識別客戶和合作夥伴。

| 名稱        | 類型   | 必要 | 描述                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| customer-id | 字串 | 是      | 識別客戶的 GUID 格式字串。       |
| mpn-id      | int    | 是      | 識別合作夥伴的 Microsoft 合作夥伴網路識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[訂](subscription-resources.md)用帳戶資源的集合。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a>另請參閱

- [合作夥伴中心分析 - 資源](partner-center-analytics-resources.md)
