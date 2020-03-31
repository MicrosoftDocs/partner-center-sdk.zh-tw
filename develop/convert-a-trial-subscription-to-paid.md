---
title: 將試用訂用帳戶轉換為付費
description: 如何將試用訂閱轉換成付費帳戶。
ms.assetid: 06EB96D7-6260-47E0-ACAE-07D4213BEBB7
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d41fa94a78d49a6537834ddaf9d4c62c54d8f911
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413557"
---
# <a name="convert-a-trial-subscription-to-paid"></a>將試用訂用帳戶轉換為付費

適用於：

- 夥伴中心

您可以將試用訂用帳戶轉換為付費。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼。
- 有效試用訂用帳戶的訂用帳戶識別碼。
- 可用的轉換供應專案。

## <a name="convert-a-trial-subscription-to-paid-through-code"></a>將試用訂用帳戶轉換為透過程式碼付費

若要將試用訂閱轉換成付費帳戶，您必須先取得可用試用轉換的集合。 然後，您必須選擇您想要購買的轉換供應專案。

轉換供應專案將指定的數量預設為與試用訂用帳戶相同的授權數目。 將[**quantity**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity)屬性設定為您要購買的授權數目，即可變更此數量。

> [!NOTE]
> 無論購買的授權數目為何，試用版的訂用帳戶 ID 都會重複用於已購買的授權。 因此，試用版會消失，並取代為購買。

使用下列步驟，透過程式碼來轉換試用訂閱：

1. 取得可用訂用帳戶作業的介面。 您必須識別客戶，並指定試用訂用帳戶的訂用帳戶識別碼。

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. 取得可用轉換供應專案的集合。 如需有關此方法的要求/回應的詳細資訊和詳細資料，請參閱[取得試用版轉換](get-a-list-of-trial-conversion-offers.md)供應專案清單。

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. 選擇轉換供應專案。 下列程式碼會選擇集合中的第一個轉換供應專案。

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. （選擇性）指定要購買的授權數目。 預設值為試用訂用帳戶中的授權數目。

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. 呼叫[**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync)方法，以將試用訂閱轉換為付費。

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

若要將試用訂閱轉換成付費帳戶：

1. 使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法搭配客戶識別碼來識別客戶。
2. 使用試用版訂用帳戶識別碼呼叫[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法，以取得訂用帳戶作業的介面。 將訂用帳戶作業介面的參考儲存在本機變數中。
3. 使用 [[**轉換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions)] 屬性來取得轉換上可用作業的介面，然後呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync)方法，以取得可用[**轉換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)供應專案的集合。 您必須選擇其中一個。 下列範例會預設為第一個可用的轉換。
4. 使用您儲存在本機變數中的訂用帳戶作業介面的參考和[**轉換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions)屬性，以取得轉換時可用作業的介面。
5. 將選取的轉換供應專案物件傳遞至[**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync)方法，以嘗試進行試用轉換。

### <a name="c-example"></a>C#實例

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

使用下列路徑參數來識別客戶和試用版訂用帳戶。

| 名稱            | 類型   | 必要項 | 描述                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| 客戶識別碼     | string | 是      | 識別客戶的 GUID 格式字串。           |
| 訂用帳戶識別碼 | string | 是      | 可識別試用訂閱的 GUID 格式字串。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

填入的[轉換](conversions-resources.md#conversion)資源必須包含在要求主體中。

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

### <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含[ConversionResult](conversions-resources.md#conversionresult)資源。

#### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心錯誤碼](error-codes.md)。

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```