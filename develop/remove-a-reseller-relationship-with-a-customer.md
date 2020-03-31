---
title: 移除與客戶的經銷商關係
description: 如何移除與您不再具有交易之客戶的轉銷商關係。
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3e64b6b9921e500d4f4926a45a624c909988ec00
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415475"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>移除與客戶的經銷商關係


**適用於**

- 夥伴中心  


移除與您不再具有交易之客戶的轉銷商關係。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼（客戶租使用者識別碼）。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- 在移除轉銷商關聯性之前，必須先取消所有 Azure 保留的 VM 實例訂單。 呼叫 Azure 支援以取消任何已開啟的 Azure 保留的 VM 實例訂單。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要移除客戶的轉銷商關聯性，您必須先確定該客戶的任何使用中 Azure 保留的 VM 執行個體已取消，且該客戶的所有使用中訂用帳戶都已暫停。 若要這麼做，請判斷您想要刪除轉銷商關係之客戶的識別碼（在下列程式碼範例中，系統會提示使用者提供客戶識別碼）。 

若要判斷是否必須取消客戶的任何 Azure 保留的 VM 執行個體，請使用客戶識別碼呼叫[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法來指定客戶，以及取得權利集合作業介面的[**權利**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)屬性，以取得權利的集合。 呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync)方法，以取出權利集合。 針對[**EntitlementType**](entitlement-resources.md#entitlementtype)值為[**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype)的任何權利篩選集合，如果有的話，請先呼叫支援以取消其，再繼續進行。 

然後，藉由呼叫[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法來指定客戶，並使用 [[**訂閱**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)] 屬性來取得訂用帳戶集合作業的介面，藉此抓取客戶的訂閱集合。 最後，呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync)方法，以取出客戶的訂用帳戶集合。 流覽訂用帳戶集合，並確定沒有訂閱[ **。 Status**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)屬性值為[**SubscriptionStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)。 如果訂用帳戶仍在使用中，請參閱暫止訂閱以取得如何暫停[訂用](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription)帳戶的相關資訊。 

確認該客戶的所有作用中 Azure 保留的 VM 執行個體都已取消，且所有作用中的訂用帳戶都已暫停之後，您就可以移除該客戶的轉銷商關係。 首先，建立新的[customer](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer)物件，並將[RelationshipToPartner](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner)屬性設定為[**CustomerPartnerRelationship。 None**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)。 然後使用客戶識別碼來呼叫[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，以指定客戶，並呼叫**Patch**方法，傳入新的 customer 物件。

若要重新建立關聯性，請重複[要求轉銷商關聯](https://docs.microsoft.com/partner-center/develop/request-reseller-relationship)性的程式。 


``` csharp
// IAggregatePartner partnerOperations;

// Prompt the user the enter the customer ID.
var customerIdToDeleteRelationshipOf = this.Context.ConsoleHelper.ReadNonEmptyString("Please enter the ID of the customer you want to delete the relationship with", "The customer ID can't be empty");

// Determine if there are any active Azure Reserved VM Instances for this customer.
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Entitlements.Get();

If (entitlements.Items.Where(x => x.EntitlementType == EntitlementType.VirtualMachineReservedInstance).Any())
{
    this.Context.ConsoleHelper.Warning("Please cancel Azure Reserved Virtual Machine Instance orders through support and try again. Aborting the delete customer relationship operation");
               return;
}

// Verify that there are no active subscriptions.
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Subscriptions.Get();
IList<Subscription> subscriptions = new List<Subscription>(customerSubscriptions.Items);

foreach (Subscription customerSubscription in subscriptions)
{
    if (customerSubscription.Status == SubscriptionStatus.Active)
    {
        this.Context.ConsoleHelper.Warning(String.Format("Subscription with ID :{0}  OfferName: {1} cannot be in active state, ", customerSubscription.Id, customerSubscription.OfferName));
        this.Context.ConsoleHelper.Warning("Please Suspend all the Subscriptions and try again. Aborting the delete customer relationship operation");
               return;
    }
}

// Delete the customer's relationship to the partner.
Customer customer = new Customer();
customer.RelationshipToPartner = CustomerPartnerRelationship.None;
customer = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Patch(customer);

if (customer.RelationshipToPartner == CustomerPartnerRelationship.None)
{
    this.Context.ConsoleHelper.Success("Customer Partner Relationship successfully deleted");
}
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSample**類別**： DeletePartnerCustomerRelationship.cs


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求   


**要求語法**

| 方法     | 要求 URI                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **跳**  | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/HTTP/1。1 |

 

**URI 參數**

下表列出移除轉銷商關聯性所需的查詢參數。

| 名稱                   | 類型     | 必要項 | 描述                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **客戶-租使用者識別碼** | **guid** | Y        | 此值是可識別客戶的 GUID 格式**客戶租使用者識別碼**。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

要求主體中需要**客戶**資源。 確定 [ **RelationshipToPartner** ] 屬性已設定為 [無]。

**要求範例**

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Content-Length: 74
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
MS-RequestId: 9fef8b23-6e3e-45d2-8678-e9fe89c35af5
Date: Fri, 12 Jan 2018 00:31:55 GMT

{
    "relationshipToPartner":"none",
    "attributes":{
        "objectType":"Customer"
    }
}
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 回應


如果成功，這個方法會移除指定之客戶的轉銷商關係。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
MS-RequestId: 7988dde4-b516-472c-b226-6d53fb18f04e
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
X-Locale: en-US
Content-Type: application/json
Content-Length: 242
Expect: 100-continue

{
    "Id":null,
    "CommerceId":null,
    "CompanyProfile":null,
    "BillingProfile":null,
    "RelationshipToPartner":"none",
    "AllowDelegatedAccess":null,
    "UserCredentials":null,
    "CustomDomains":null,
    "AssociatedPartnerId":null,
    "Attributes":{
        "ObjectType":"Customer"
    }
}
```