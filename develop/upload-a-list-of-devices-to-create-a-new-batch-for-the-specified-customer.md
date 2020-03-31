---
title: 上傳裝置清單，為指定的客戶建立新的批次
description: 如何上傳裝置的相關資訊清單，為指定的客戶建立新的批次。 這會建立裝置批次以進行免觸控部署的註冊，並將裝置和裝置批次與指定的客戶產生關聯。
ms.assetid: 94DB98F2-2188-46BB-97BA-100B8C94F120
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ace97d2f225471b01c3b6973f222d33b0795c761
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414461"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a>上傳裝置清單，為指定的客戶建立新的批次

適用於：

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何上傳裝置的相關資訊清單，為指定的客戶建立新的批次。 這會建立裝置批次以進行免觸控部署的註冊，並將裝置和裝置批次與指定的客戶產生關聯。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用應用程式加上使用者的認證來進行驗證。 搭配合作夥伴中心 Api 使用應用程式 + 使用者驗證時，請遵循[安全的應用程式模型](enable-secure-app-model.md)。
- 客戶識別碼。
- 提供個別裝置相關資訊的裝置資源清單。

## <a name="c"></a>C\#

若要上傳裝置清單以建立新的裝置批次：

1. 具現化[**裝置**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device)類型的新[清單](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)，並將裝置填入清單。 識別每個裝置至少需要下列已填入屬性的組合：

    - [**HardwareHash**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)。
    - [**HardwareHash**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)。
    - [**HardwareHash**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)。
    - 僅限[**HardwareHash**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) 。
    - 僅限[**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) 。
    - [**SerialNumber**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname)。

2. 具現化[**DeviceBatchCreationRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest)物件，並將[**BatchId**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid)屬性設定為您所選擇的唯一名稱，並將[**devices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices)屬性設為要上傳的裝置清單。

3. 藉由呼叫[**iaggregatepartner.customers.byid. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法與客戶識別碼來處理裝置批次建立要求，以取得指定客戶上作業的介面。

4. 使用裝置批次建立要求來呼叫[**DeviceBatches**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection)方法，以建立批次。

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

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： CreateDeviceBatch.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1。1 |

#### <a name="uri-parameter"></a>URI 參數

建立要求時，請使用下列路徑參數。

| 名稱        | 類型   | 必要項 | 描述                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 客戶識別碼 | string | 是      | 識別客戶的 GUID 格式字串。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

要求主體必須包含[DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest)資源。

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

如果成功，回應會包含一個**位置**標頭，其中具有可用於抓取裝置上傳狀態的 URI。 儲存此 URI 以與其他相關的 REST Api 搭配使用。

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
