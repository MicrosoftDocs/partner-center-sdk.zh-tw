---
title: 更新訂用帳戶的暱稱
description: 更新客戶訂用帳戶的易記名稱或昵稱。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fc17e1ff2b38b2280c1f1bdb6baf14df2c5e645b
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925603"
---
# <a name="update-the-nickname-for-a-subscription"></a>更新訂用帳戶的暱稱

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

更新客戶 [訂](subscription-resources.md)用帳戶的易記名稱或昵稱。 此名稱會出現在合作夥伴中心中，以協助區分客戶帳戶中的訂閱。

在合作夥伴中心儀表板中，您可以先 [選取客戶](get-a-customer-by-name.md)來執行這項作業。 然後，選取您要重新命名的訂用帳戶。 若要完成，請變更 [訂用帳戶 **昵稱** ] 欄位中的名稱，然後選取 [ **提交]。**

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 訂用帳戶識別碼。

## <a name="c"></a>C\#

若要更新客戶訂用帳戶的昵稱，請先 [取得訂](get-a-subscription-by-id.md)用帳戶，然後變更訂用帳戶的 [**FriendlyName**/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) 屬性。 進行變更之後，請使用您的 [**>ipartner.customers. Customers**/dotnet/api/microsoft.store.partnercenter.ipartner.customers) 集合，並呼叫 [**>iaggregatepartner.customers.byid ( # B2 **/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法。 然後，呼叫 [**訂閱**/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) 屬性，後面接著 [**>iaggregatepartner.customers.byid ( # B2 **/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) 方法。 然後，藉由呼叫 [**Patch ( # B1 **/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) 方法來完成。

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSamples **類別**： UpdateSubscription.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法    | 要求 URI                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **補丁** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

下表列出更新訂用帳戶昵稱的必要查詢參數。

| 名稱                    | 類型     | 必要 | 描述                          |
|-------------------------|----------|----------|--------------------------------------|
| **customer-tenant-id**  | **guid** | Y        |  (GUID) 的 **客戶租使用者識別碼** 。 |
| **id-for-subscription** | **guid** | Y        |  (GUID) 的訂用帳戶識別碼。        |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求本文中必須有完整的 **Subscription** 資源。 確定 [ **FriendlyName** ] 屬性已更新。

### <a name="request-example"></a>要求範例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "<subscriptionID>",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回更新的 [訂](subscription-resources.md) 用帳戶資源屬性。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "<subscriptionID>",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
