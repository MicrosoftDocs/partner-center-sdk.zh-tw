---
title: Device deployment resources
description: Resources related to Partner Center device deployment.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1aecf66907d8e39ae3015ba7a7735942555d1d1c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489948"
---
# <a name="device-deployment-resources"></a>Device deployment resources

適用於：

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

The following resources are related to device deployment.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** provides information about a configuration policy.

| 屬性             | 在工作列搜尋方塊中輸入                                                           | 說明                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | 字串                                       | A GUID-formatted string that identifies the policy.                                  |
| name                 | 字串                                       | The friendly name for the policy.                                                    |
| 類別             | 字串                                       | The category.                                                                        |
| 描述          | 字串                                       | The policy description.                                                              |
| devicesAssignedCount | 數目                                       | The number of devices assigned to this policy.                                       |
| policySettings       | array of strings                             | The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip\_oem\_registration", "skip\_eula".    |
| createdDate          | string in UTC date-time format               | The date and time the policy was created.                                            |
| lastModifiedDate     | string in UTC date-time format               | The date and time the policy was last modified.                                      |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                            |

## <a name="device"></a>裝置

**Device** provides information about a device.

| 屬性            | 在工作列搜尋方塊中輸入                                                           | 說明                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | 字串                                                         | A GUID-formatted string that identifies the device.                      |
| serialNumber        | 字串                                                         | The serial number uniquely associated with the device.                   |
| productKey          | 字串                                                         | The product key uniquely associated with the device.                     |
| hardwareHash        | 字串                                                         | The hardware hash uniquely associated with the device.                   |
| modelName           | 字串                                                         | The model name associated with the device.                               |
| oemManufacturerName | 字串                                                         | The name of the OEM manufacturer associated with the device.             |
| 原則            | array of objects                                               | The list of policies assigned to the device.                             |
| uploadedDate        | string in UTC date-time format                                 | The date and time the device details were uploaded.                      |
| allowedOperations   | array of strings                                               | The list of HTTP methods allowed on a device sync as GET, PATCH, DELETE. |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** describes the status of a device batch upload of information about each device in a list of devices.

| 屬性        | 在工作列搜尋方塊中輸入     | 說明                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | 字串   | A GUID-formatted string that is associated with the batch of devices uploaded. |
| 狀態          | 字串   | The status of the batch upload: "unknown","queued","processing","finished","finished\_with\_errors". |
| startedTime     | string in UTC date-time format | The date and time that the batch upload process started.   |
| completedTime   | string in UTC date-time format  | The date and time that the batch upload process completed.   |
| devicesStatus   | array of [DeviceUploadDetails](#deviceuploaddetails) resources | An array of objects that specify the status of each device information upload. |
| 屬性      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** describes the status of an upload of information about a device.

| 屬性         | 在工作列搜尋方塊中輸入                    | 說明                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | 字串                  | A GUID-formatted string that is associated with the device. |
| serialNumber     | 字串                  | The serial number uniquely associated with the device. |
| productKey       | 字串                  | The product key uniquely associated with the device. |
| 狀態           | 字串                  | The status of the device information upload: "in-progress", "finished", "finished\_with\_errors". |
| errorCode        | 字串                  | The HTTP status error code returned if the device upload fails. |
| errorDescription | 字串                  | The HTTP error description if the device upload fails. |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** represents a collection of devices.

| 屬性     | 在工作列搜尋方塊中輸入                                                           | 說明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | 字串                                                         | A GUID-formatted string that is associated with the batch of devices. |
| createdBy    | 字串                                                         | The name of the tenant that created the collection.                   |
| creationDate | string in UTC date-time format                                 | The data and time that the collection was created.                    |
| deviceCount  | 數目                                                         | The number of devices in the collection.                              |
| devicesLink  | [連結](utility-resources.md#link)                              | A link to the devices contained in this batch.                        |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** provides the information required to create a device batch and populates it with devices.

| 屬性     | 在工作列搜尋方塊中輸入                                                           | 說明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | 字串                                                         | A GUID-formatted string that is associated with the batch of devices. |
| 裝置      | array of [Device](#device) objects                             | Each object specifies a device. The following combinations of fields for identifying a device are accepted: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash only, productKey only, serialNumber + oemManufacturerName + modelName. |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** provides the information required to update a list of devices with a policy.

| 屬性     | 在工作列搜尋方塊中輸入                                                           | 說明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| 裝置      | array of [Device](#device) objects                             | Each object specifies a device. The following properties are required: Id, Policies. |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |
