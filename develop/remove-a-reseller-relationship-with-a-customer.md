---
title: 移除與客戶的經銷商關係
description: 如何移除與您不再具有交易之客戶的轉銷商關係。
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 00ab4361c7eb83ea14b52d7858ecb8f04b5c7550
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157020"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>移除與客戶的經銷商關係

**適用于**

- 合作夥伴中心

移除與您不再具有交易之客戶的轉銷商關係。

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用應用程式 + 使用者認證進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

- 在移除轉銷商關聯性之前，必須先取消所有 Azure 保留的 VM 實例訂單。 呼叫 Azure 支援以取消任何已開啟的 Azure 保留的 VM 實例訂單。

## <a name="c"></a>C\#

若要移除客戶的轉銷商關聯性，請先確定已取消該客戶的任何使用中 Azure 保留的 VM 執行個體。 接下來，請確定該客戶的所有作用中訂用帳戶都已暫停。 若要這麼做，請決定您想要刪除轉銷商關係的客戶識別碼。 在下列程式碼範例中，系統會提示使用者提供客戶識別碼。

若要判斷是否必須取消客戶的任何 Azure 保留的 VM 執行個體，請使用客戶識別碼呼叫[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法來指定客戶，以及取得權利集合作業介面的[**權利**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)屬性，以取得權利的集合。 呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync)方法，以取出權利集合。 針對[**EntitlementType**](entitlement-resources.md#entitlementtype)值為[**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype)的任何權利篩選集合，如果有的話，請先呼叫支援以取消其，再繼續進行。

然後，藉由呼叫[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法來指定客戶，並使用 [[**訂閱**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)] 屬性來取得訂用帳戶集合作業的介面，藉此抓取客戶的訂閱集合。 最後，呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync)方法，以取出客戶的訂用帳戶集合。 流覽訂用帳戶集合，並確定沒有訂閱[**。 Status**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)屬性值為[**SubscriptionStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)。 如果訂用帳戶仍在使用中，請參閱暫止訂閱以取得如何暫停[訂用](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription)帳戶的相關資訊。

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

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **跳**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

下表列出移除轉銷商關聯性所需的查詢參數。

| 名稱                   | 類型     | 必要 | 描述                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 此值是可識別客戶的 GUID 格式**客戶租使用者識別碼**。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求主體中需要**客戶**資源。 確定 [ **RelationshipToPartner** ] 屬性已設定為 [無]。

### <a name="request-example"></a>要求範例

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

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會移除指定之客戶的轉銷商關係。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

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
