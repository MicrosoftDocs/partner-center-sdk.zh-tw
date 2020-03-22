---
title: 裝置部署資源
description: 與合作夥伴中心裝置部署相關的資源。
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1aecf66907d8e39ae3015ba7a7735942555d1d1c
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083155"
---
# <a name="device-deployment-resources"></a>裝置部署資源

適用於：

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心

下列資源與裝置部署相關。

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy**提供設定原則的相關資訊。

| 屬性             | 類型                                                           | 描述                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | string                                       | 可識別原則的 GUID 格式字串。                                  |
| 名稱                 | string                                       | 原則的易記名稱。                                                    |
| category             | string                                       | 類別。                                                                        |
| 描述          | string                                       | 原則描述。                                                              |
| devicesAssignedCount | 數字                                       | 指派給此原則的裝置數目。                                       |
| policySettings       | 字串的陣列                             | 原則設定： [無]、[移除\_oem\_預先安裝]、[oobe\_使用者\_不\_本機\_系統管理員]、[略過\_express\_設定]、[略過\_oem\_註冊]、[略過\_的授權合約]。    |
| createdDate          | UTC 日期時間格式的字串               | 建立原則的日期和時間。                                            |
| lastModifiedDate     | UTC 日期時間格式的字串               | 上次修改原則的日期和時間。                                      |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                            |

## <a name="device"></a>裝置

**裝置**提供裝置的相關資訊。

| 屬性            | 類型                                                           | 描述                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | string                                                         | GUID 格式的字串，可識別裝置。                      |
| serialNumber        | string                                                         | 與裝置唯一相關聯的序號。                   |
| productKey          | string                                                         | 與裝置唯一相關聯的產品金鑰。                     |
| hardwareHash        | string                                                         | 唯一與裝置相關聯的硬體雜湊。                   |
| modelName           | string                                                         | 與裝置相關聯的模型名稱。                               |
| oemManufacturerName | string                                                         | 與裝置相關聯的 OEM 製造商名稱。             |
| 原則            | 物件的陣列                                               | 指派給裝置的原則清單。                             |
| uploadedDate        | UTC 日期時間格式的字串                                 | 裝置詳細資料上傳的日期和時間。                      |
| allowedOperations   | 字串的陣列                                               | 裝置同步處理所允許的 HTTP 方法清單，例如 GET、PATCH、DELETE。 |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails**描述裝置批次上傳裝置清單中每個裝置的相關資訊的狀態。

| 屬性        | 類型     | 描述                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | string   | GUID 格式的字串，與上傳的裝置批次相關聯。 |
| status          | string   | 批次上傳的狀態：「不明」、「已排入佇列」、「處理中」、「已完成」、「已完成\_，但發生\_錯誤」。 |
| startedTime     | UTC 日期時間格式的字串 | 批次上傳程式開始的日期和時間。   |
| completedTime   | UTC 日期時間格式的字串  | 批次上傳程式完成的日期和時間。   |
| devicesStatus   | [DeviceUploadDetails](#deviceuploaddetails)資源的陣列 | 物件的陣列，指定每個裝置資訊上傳的狀態。 |
| 屬性      | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails**描述上傳裝置相關資訊的狀態。

| 屬性         | 類型                    | 描述                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | string                  | 與裝置相關聯的 GUID 格式字串。 |
| serialNumber     | string                  | 與裝置唯一相關聯的序號。 |
| productKey       | string                  | 與裝置唯一相關聯的產品金鑰。 |
| status           | string                  | 裝置資訊上傳的狀態：「進行中」、「已完成」、「已完成\_，但發生\_錯誤」。 |
| errorCode        | string                  | 當裝置上傳失敗時傳回的 HTTP 狀態錯誤碼。 |
| errorDescription | string                  | 如果裝置上傳失敗，則為 HTTP 錯誤描述。 |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch**代表裝置的集合。

| 屬性     | 類型                                                           | 描述                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | string                                                         | 與裝置批次相關聯的 GUID 格式字串。 |
| createdBy    | string                                                         | 建立集合的租使用者名稱。                   |
| creationDate | UTC 日期時間格式的字串                                 | 建立集合的資料和時間。                    |
| deviceCount  | 數字                                                         | 集合中的裝置數目。                              |
| devicesLink  | [連結](utility-resources.md#link)                              | 包含在此批次中的裝置連結。                        |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest**提供建立裝置批次並在其中填入裝置所需的資訊。

| 屬性     | 類型                                                           | 描述                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | string                                                         | 與裝置批次相關聯的 GUID 格式字串。 |
| devices      | [裝置](#device)物件的陣列                             | 每個物件都會指定一個裝置。 已接受下列用於識別裝置的欄位組合： hardwareHash + productKey、hardwareHash + serialNumber、hardwareHash + productKey + serialNumber、hardwareHash only、僅 productKey、serialNumber + oemManufacturerName +modelName. |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest**提供使用原則更新裝置清單所需的資訊。

| 屬性     | 類型                                                           | 描述                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | [裝置](#device)物件的陣列                             | 每個物件都會指定一個裝置。 需要下列屬性：識別碼、原則。 |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                              |
