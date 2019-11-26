---
title: 使用原則更新裝置清單
description: 如何使用指定客戶的設定原則來更新裝置清單。
ms.assetid: D68DAE8B-EFBC-4C71-8CB4-3ADA8D45DDBA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: bcc89cbab22371cddf374367a3753fe6d137ec59
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486408"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>使用原則更新裝置清單


**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何使用指定客戶的設定原則來更新裝置清單。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼。
- 原則識別碼。
- 要更新之裝置的裝置識別碼。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要使用指定的設定原則更新裝置清單，請先將[KeyValuePair](https://docs.microsoft.com/dotnet/api/system.collections.generic.keyvaluepair-2)[ **（PolicyCategory，** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String）類型的[清單](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)具現化，並新增要套用的原則，如下列程式碼範例所示。 您將需要原則的原則識別碼。

然後，建立要使用原則更新的[**裝置**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device)物件清單，並指定裝置識別碼和包含要套用之原則的清單（適用于每個裝置）。 接下來，將[**DevicePolicyUpdateRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest)物件具現化，並將[**Devices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices)屬性設定為裝置物件的清單。

若要處理裝置原則更新要求，請使用客戶識別碼呼叫[**Iaggregatepartner.customers.byid ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，以在指定的客戶上取得作業介面。 然後，取出[**DevicePolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy)屬性，以取得客戶裝置集合作業的介面。 最後，使用 DevicePolicyUpdateRequest 物件呼叫[**update**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update)方法，以使用原則來更新裝置。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId; 
string selectedDeviceId;

// Indicate the policy to apply to the list of devices. 
List<KeyValuePair<PolicyCategory, string>> 
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest 
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices             
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation = 
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： UpdateDevicesPolicy.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法    | 要求 URI                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **跳** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1。1 |

 

**URI 參數**

建立要求時，請使用下列路徑參數。

| 名稱        | 類型   | 必要 | 描述                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 客戶識別碼 | 字串 | 是      | 識別客戶的 GUID 格式字串。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

要求主體必須包含[DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest)資源。

**要求範例**

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應會包含一個**位置**標頭，其中具有可用於抓取此批次進程狀態的 URI。 儲存此 URI 以與其他相關的 REST Api 搭配使用。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```

 

 




