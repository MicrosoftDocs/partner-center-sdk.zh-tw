---
title: 將裝置清單上傳至指定客戶的現有批次
description: 如何將裝置的相關資訊清單上傳至指定之客戶的現有批次。 這會將裝置與已建立的裝置批次建立關聯。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a3f6522b31d296e10c66cb45b3684eae3e0c25ab
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926436"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>將裝置清單上傳至指定客戶的現有批次

**適用於**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何將裝置的相關資訊清單上傳至指定之客戶的現有批次。 這會將裝置與已建立的裝置批次建立關聯。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 裝置批次識別碼。

- 提供個別裝置相關資訊的裝置資源清單。

## <a name="c"></a>C\#

若要將裝置清單上傳至現有的裝置批次，請先將新的 [清單/dotnet/api/-1) 具現化 [**裝置**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) ]，然後在清單中填入裝置。 下列填入的屬性組合至少需要用來識別每個裝置：

- [**HardwareHash**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) 。

- [**HardwareHash**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) 。

- [**HardwareHash**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**/Dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) 。

- [僅限**HardwareHash**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) 。

- [僅限**ProductKey**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) 。

- [**SerialNumber**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**/Dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname) 。

然後，使用客戶識別碼來呼叫 [**>iaggregatepartner.customers. >iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法，以取得指定客戶上作業的介面。 接下來，使用裝置批次識別碼來呼叫 [**DeviceBatches. >iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) 方法，以取得指定批次作業的介面。 最後，呼叫 [**devices. 建立**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) 或 [**CreateAsync**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync]) 方法，並使用裝置清單將裝置新增至裝置批次。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： CreateDevices.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1。1 |

### <a name="uri-parameter"></a>URI 參數

建立要求時，請使用下列路徑和查詢參數。

| 名稱           | 類型   | 必要 | 描述                                           |
|----------------|--------|----------|-------------------------------------------------------|
| customer-id    | 字串 | Yes      | 用來識別客戶的 GUID 格式字串。 |
| devicebatch-id | 字串 | Yes      | 識別裝置批次的字串識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求主體必須包含 [裝置](device-deployment-resources.md#device) 物件的陣列。 接受下列識別裝置的欄位組合：

- hardwareHash + productKey。
- hardwareHash + serialNumber。
- hardwareHash + productKey + serialNumber。
- 僅限 hardwareHash。
- 僅限 productKey。
- serialNumber + oemManufacturerName + modelName。

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a>REST 回應

如果成功，回應會包含具有 URI 的 **位置** 標頭，可用來取得裝置上傳狀態。 儲存此 URI 以搭配其他相關 REST Api 使用。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
