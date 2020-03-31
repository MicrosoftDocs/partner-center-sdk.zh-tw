---
title: 將裝置清單上傳至指定客戶的現有批次
description: 如何將裝置的相關資訊清單上傳至指定客戶的現有批次。 這會使裝置與已建立的裝置批次產生關聯。
ms.assetid: 5EC2895C-1361-4EBA-9D86-7125D4FE10D3
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 849f88b43737cbb61908a45b2e53213099e89871
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414475"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>將裝置清單上傳至指定客戶的現有批次


**適用於**

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何將裝置的相關資訊清單上傳至指定客戶的現有批次。 這會使裝置與已建立的裝置批次產生關聯。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼。
- 裝置批次識別碼。
- 提供個別裝置相關資訊的裝置資源清單。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要將裝置清單上傳至現有的裝置批次，請先具現化裝置[**類型的**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device)新[清單](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)，並在清單中填入裝置。 識別每個裝置至少需要下列已填入屬性的組合：

- [**HardwareHash**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)。
- [**HardwareHash**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)。
- [**HardwareHash**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)。
- 僅限[**HardwareHash**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) 。
- 僅限[**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) 。
- [**SerialNumber**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname)。

然後，使用客戶識別碼呼叫[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，以在指定的客戶上取得作業的介面。 接下來，使用裝置批次識別碼呼叫[**DeviceBatches. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid)方法，以取得指定批次之作業的介面。 最後，使用裝置清單來呼叫[**devices. Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create)或[**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync)方法，以將裝置新增至裝置批次。

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

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： CreateDevices.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法   | 要求 URI                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1。1 |

 

**URI 參數**

建立要求時，請使用下列路徑和查詢參數。

| 名稱           | 類型   | 必要項 | 描述                                           |
|----------------|--------|----------|-------------------------------------------------------|
| 客戶識別碼    | string | 是      | 識別客戶的 GUID 格式字串。 |
| devicebatch-id | string | 是      | 識別裝置批次的字串識別碼。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

要求主體必須包含[裝置](device-deployment-resources.md#device)物件的陣列。 已接受下列用於識別裝置的欄位組合：

- hardwareHash + productKey。
- hardwareHash + serialNumber。
- hardwareHash + productKey + serialNumber。
- 僅限 hardwareHash。
- 僅限 productKey。
- serialNumber + oemManufacturerName + modelName。

**要求範例**

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

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應會包含一個**位置**標頭，其中具有可用於抓取裝置上傳狀態的 URI。 儲存此 URI 以與其他相關的 REST Api 搭配使用。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

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

 

 




