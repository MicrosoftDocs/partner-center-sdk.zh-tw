---
title: 指派授權給使用者
description: 如何將授權指派給客戶使用者。
ms.assetid: 872C7444-DF89-4EB5-8C1E-1D8E2934A40E
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1f968ce90d4bbed3f3c9384b82c70a9ee7811f71
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413225"
---
# <a name="assign-licenses-to-a-user"></a>指派授權給使用者

適用於：

- 夥伴中心

如何將授權指派給客戶使用者。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 客戶識別碼。 客戶應具有可指派授權的訂用帳戶。
- 客戶的使用者識別碼。 這會識別要指派授權的使用者。
- 識別授權產品的產品 SKU 識別碼。

## <a name="assigning-licenses-through-code"></a>透過程式碼指派授權

當您將授權指派給使用者時，您必須從客戶的已訂閱 Sku 集合中進行選擇。 然後，在識別出您要指派的產品之後，您必須取得每個產品的產品 SKU 識別碼，才能進行指派。 每個[**SubscribedSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku)實例都包含[**ProductSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku)屬性，您可以從中參考[**ProductSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku)物件並取得[**識別碼**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)。

授權指派要求必須包含來自單一授權群組的授權。 例如，您無法在相同的要求中，從[**Group1**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)和**Group2**指派授權。 在單一要求中，嘗試從一個以上的群組指派授權將會失敗，並產生適當的錯誤。 若要瞭解授權群組可用的授權，請參閱[依授權群組取得可用的授權清單](get-a-list-of-available-licenses-by-license-group.md)。

以下是透過程式碼指派授權的步驟：

1. 具現化[**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)物件。 您可以使用此物件來指定要指派的產品 SKU 和服務方案。

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. 填入物件屬性，如下所示。 此程式碼假設您已經有產品 SKU 識別碼，而且將會指派所有可用的服務方案（亦即不會排除任何）。
  
    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. 如果您沒有產品 SKU 識別碼，則必須取出已訂閱的 Sku 集合，並從其中一個取得產品 SKU 識別碼。 如果您知道產品 SKU 名稱，以下是範例。

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. 接下來，將[**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)類型的新清單具現化，並新增授權物件。 您可以將每個授權分別新增至清單，以指派多個授權。 此清單中包含的授權必須來自相同的授權群組。

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. 建立[**LicenseUpdate**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate)實例，並將授權指派清單指派給[**LicensesToAssign**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)屬性。

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. 呼叫[**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync)方法，並傳遞如下所示的授權更新物件來指派授權。

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

若要將授權指派給客戶使用者，請先將[**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)物件具現化，並填入[**Skuid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid)和[**ExcludedPlans**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans)屬性。 您可以使用此物件來指定要指派的產品 SKU，以及要排除的服務方案。 接下來，將**LicenseAssignment**類型的新清單具現化，並將授權物件新增至清單。 然後建立[**LicenseUpdate**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate)實例，並將授權指派清單指派給[**LicensesToAssign**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)屬性。

接下來，使用[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法搭配客戶識別碼來識別客戶，並搭配使用[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)方法和使用者識別碼來識別使用者。 然後從[**LicenseUpdates**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates)屬性取得客戶使用授權更新作業的介面。

最後，呼叫[**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync)方法，並傳遞授權更新物件來指派授權。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： CustomerUserAssignLicenses.cs

## <a name="request"></a>要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

使用下列 path 參數來識別客戶和使用者。

| 名稱        | 類型   | 必要項 | 描述                                       |
|-------------|--------|----------|---------------------------------------------------|
| 客戶識別碼 | string | 是      | 識別客戶的 GUID 格式識別碼。 |
| user-id     | string | 是      | 識別使用者的 GUID 格式化識別碼。     |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

您必須在要求主體中包含[LicenseUpdate](license-resources.md#licenseupdate)資源，以指定要指派的授權。

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，則會傳回 HTTP 回應狀態碼201，且回應主體會包含具有授權資訊的[LicenseUpdate](license-resources.md#licenseupdate)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example-success"></a>回應範例 (成功)

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-is-not-available"></a>回應範例（授權無法使用）

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```