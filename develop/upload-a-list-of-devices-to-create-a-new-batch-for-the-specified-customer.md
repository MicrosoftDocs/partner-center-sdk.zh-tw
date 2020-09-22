---
title: 上傳裝置清單，為指定的客戶建立新的批次
description: 如何上傳有關裝置的資訊清單，以為指定的客戶建立新的批次。 這會建立裝置批次以進行免觸控部署的註冊，並將裝置和裝置批次與指定的客戶產生關聯。
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 68ae21fa790b3c0810e26c54860b83d1ab303b8c
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927875"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a>上傳裝置清單，為指定的客戶建立新的批次

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何上傳有關裝置的資訊清單，以為指定的客戶建立新的批次。 這會建立裝置批次以進行免觸控部署的註冊，並將裝置和裝置批次與指定的客戶產生關聯。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。 使用應用程式 + 使用者驗證搭配合作夥伴中心 Api 時，請遵循 [安全的應用程式模型](enable-secure-app-model.md) 。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 提供個別裝置相關資訊的裝置資源清單。

## <a name="c"></a>C\#

若要上傳裝置清單以建立新的裝置批次：

1. 具現化新的 [清單/dotnet/api/-1) 類型 [**裝置**) /dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device]，並在清單中填入裝置。 下列填入的屬性組合至少需要用來識別每個裝置：

   - [**HardwareHash**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) 。
   - [**HardwareHash**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) 。
   - [**HardwareHash**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**/Dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) 。
   - [僅限**HardwareHash**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) 。
   - [僅限**ProductKey**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) 。
   - [**SerialNumber**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**/Dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname) 。

2. 具現化 [**DeviceBatchCreationRequest**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) 物件，並將 [**BatchId**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.bat子) ] 屬性設定為您選擇的唯一名稱，並將 [**devices**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) ] 屬性設定為要上傳的裝置清單。

3. 藉由呼叫 [**>iaggregatepartner.customers**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法與客戶識別碼來處理裝置批次建立要求，以取得指定客戶的作業介面。

4. 使用建立批次的裝置批次建立要求，呼叫 [**DeviceBatches 建立**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) 或 [**CreateAsync**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) 方法。

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： CreateDeviceBatch.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

建立要求時，請使用下列路徑參數。

| 名稱        | 類型   | 必要 | 描述                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | 字串 | Yes      | 用來識別客戶的 GUID 格式字串。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求主體必須包含 [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) 資源。

### <a name="request-example"></a>要求範例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a>REST 回應

如果成功，回應會包含具有 URI 的 **位置** 標頭，可用來取得裝置上傳狀態。 儲存此 URI 以搭配其他相關 REST Api 使用。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

#### <a name="response-example"></a>回應範例

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```
