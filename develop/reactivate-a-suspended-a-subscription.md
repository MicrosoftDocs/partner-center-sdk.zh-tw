---
title: 重新啟用已暫停的訂用帳戶
description: 重新啟動先前已暫止因為未付款的訂用帳戶。在合作夥伴中心儀表板中，您可以先選取客戶來執行這項作業。
ms.assetid: BA30B220-C67D-4795-ACB7-7FE22B0B0F63
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f796bf70dff782275dedcf15a99e17650ac7aa2e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415516"
---
# <a name="reactivate-a-suspended-subscription"></a>重新啟用已暫停的訂用帳戶


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

重新啟動先前已暫止因為未付款的[訂](subscription-resources.md)用帳戶。

在合作夥伴中心儀表板中，您可以先[選取客戶](get-a-customer-by-name.md)來執行這項作業。 然後，選取您想要重新命名的訂用帳戶。 若要完成，請選擇 **[使用中**] 按鈕，然後選取 [提交] **。**

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- 訂用帳戶識別碼。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要重新啟用客戶的訂用帳戶，請先[取得訂](get-a-subscription-by-id.md)用帳戶，然後變更訂用帳戶的 [[**狀態**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)] 屬性。 如需**狀態**代碼的詳細資訊，請參閱[SubscriptionStatus 列舉](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)。 進行變更之後，請使用[**ipartner.getinvoices. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers)集合，並呼叫[**ById （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法。 然後呼叫[**訂閱**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)屬性，後面接著[**ById （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)方法。 然後，藉由呼叫[**Patch （）** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)方法來完成。

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： FeatureSamplesApplication。 **類別**： UpdateSubscription

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求語法**

| 方法    | 要求 URI                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **跳** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1。1 |

 

**URI 參數**

下表列出重新開機訂閱所需的查詢參數。

| 名稱                    | 類型     | 必要項 | 描述                               |
|-------------------------|----------|----------|-------------------------------------------|
| **客戶-租使用者識別碼**  | **guid** | Y        | 對應至客戶的 GUID。     |
| **訂用帳戶的識別碼** | **guid** | Y        | 對應至訂用帳戶的 GUID。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

要求主體中需要完整的**訂**用帳戶資源。 請確定 [**狀態**] 屬性已更新。

**要求範例**

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
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
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 回應


如果成功，此方法會在回應本文中傳回已更新的[訂](subscription-resources.md)用帳戶資源屬性。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

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
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
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

 

 




