---
title: 從整合沙箱中刪除客戶帳戶
description: 如何從生產環境中的測試刪除客戶帳戶 (提示) 整合沙箱。
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dc2ffbf79116b3de03b4f06656309c920868cef4
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927828"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>從整合沙箱中刪除客戶帳戶

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本文說明如何從生產環境中的測試 (提示) 整合沙箱中刪除客戶帳戶。

> [!IMPORTANT]
> 當您刪除客戶帳戶時，將會清除與該客戶租使用者相關聯的所有資源。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 從 Tip integration sandbox 刪除客戶之前，必須先取消所有 Azure 保留的虛擬機器執行個體和軟體採購訂單。

## <a name="c"></a>C\#

若要從 Tip integration sandbox 刪除客戶：

1. 將您的秘訣帳號憑證傳遞給 [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) 方法，以取得夥伴作業的 [**>ipartner.customers**](/dotnet/api/microsoft.store.partnercenter.ipartner) 介面。

2. 使用「夥伴操作」介面取出權利的集合：

    1. 使用客戶識別碼呼叫 [**>iaggregatepartner.customers.byid ( # B1 **](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法來指定客戶。

    2. 呼叫 **權利** 屬性。

    3. 呼叫 **Get** 或 **GetAsync** 方法，以取得 [**權利**](entitlement-resources.md) 集合。

3. 請確定該客戶的所有 Azure 保留的虛擬機器執行個體和軟體採購單都已取消。 針對集合中的每個 [**權利**](entitlement-resources.md) ：

    1. 使用 [**權利。ReferenceOrder.Id**](entitlement-resources.md#referenceorder) 可從客戶的訂單集合取得對應 [訂單](order-resources.md#order) 的本機複本。

    2. 將 [ [**Status**](order-resources.md#order) ] 屬性設定為 [已取消]。

    3. 使用 **Patch ( # B1 ** 方法來更新順序。

4. 取消所有訂單。 例如，下列程式碼範例會使用迴圈來輪詢每個訂單，直到其狀態為「已取消」。

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were cancelled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. 藉由呼叫客戶的 **Delete** 方法，確定所有訂單都已取消。

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 PartnerCenterSDK. FeaturesSamples **類別**： DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| 刪除     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

使用下列查詢參數來刪除客戶。

| 名稱                   | 類型     | 必要 | 說明                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| customer-tenant-id     | GUID     | Y        | 此值是 GUID 格式的 **客戶租使用者識別碼** ，可讓轉銷商針對屬於轉售商的特定客戶篩選結果。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a>REST 回應

如果成功，這個方法會傳回空的回應。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
