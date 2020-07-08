---
title: 裝置部署資源
description: 與合作夥伴中心裝置部署相關的資源。
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a464cdad3979c305df16a3bdc9133ce70a7ac688
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094106"
---
# <a name="device-deployment-resources"></a>裝置部署資源

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

下列資源與裝置部署相關。

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy**提供設定原則的相關資訊。

| 屬性             | 類型                                                           | 描述                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | 字串                                       | 可識別原則的 GUID 格式字串。                                  |
| NAME                 | 字串                                       | 原則的易記名稱。                                                    |
| category             | 字串                                       | 類別目錄。                                                                        |
| description          | 字串                                       | 原則描述。                                                              |
| devicesAssignedCount | number                                       | 指派給此原則的裝置數目。                                       |
| policySettings       | 字串陣列                             | 原則設定： [無]、[移除 \_ oem \_ 預先安裝]、[oobe \_ 使用者不是本機系統 \_ \_ \_ 管理員]、[略過 \_ 快速 \_ 設定]、[略過 \_ oem \_ 註冊]、[略過 \_ eula]。    |
| createdDate          | UTC 日期時間格式的字串               | 建立原則的日期和時間。                                            |
| lastModifiedDate     | UTC 日期時間格式的字串               | 上次修改原則的日期和時間。                                      |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                            |

## <a name="device"></a>裝置

**裝置**提供裝置的相關資訊。

| 屬性            | 類型                                                           | 描述                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | 字串                                                         | GUID 格式的字串，可識別裝置。                      |
| serialNumber        | 字串                                                         | 與裝置唯一相關聯的序號。                   |
| productKey          | 字串                                                         | 與裝置唯一相關聯的產品金鑰。                     |
| hardwareHash        | 字串                                                         | 唯一與裝置相關聯的硬體雜湊。                   |
| modelName           | 字串                                                         | 與裝置相關聯的模型名稱。                               |
| oemManufacturerName | 字串                                                         | 與裝置相關聯的 OEM 製造商名稱。             |
| 原則            | 物件的陣列                                               | 指派給裝置的原則清單。                             |
| uploadedDate        | UTC 日期時間格式的字串                                 | 裝置詳細資料上傳的日期和時間。                      |
| allowedOperations   | 字串陣列                                               | 裝置同步處理所允許的 HTTP 方法清單，例如 GET、PATCH、DELETE。 |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails**描述裝置批次上傳裝置清單中每個裝置的相關資訊的狀態。

| 屬性        | 類型     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | 字串   | GUID 格式的字串，與上傳的裝置批次相關聯。 |
| status          | 字串   | 批次上傳的狀態：「不明」、「已排入佇列」、「處理中」、「已完成」、「已完成 \_ 但 \_ 發生錯誤」。 |
| startedTime     | UTC 日期時間格式的字串 | 批次上傳程式開始的日期和時間。   |
| completedTime   | UTC 日期時間格式的字串  | 批次上傳程式完成的日期和時間。   |
| devicesStatus   | [DeviceUploadDetails](#deviceuploaddetails)資源的陣列 | 物件的陣列，指定每個裝置資訊上傳的狀態。 |
| 屬性      | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails**描述上傳裝置相關資訊的狀態。

| 屬性         | 類型                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | 字串                  | 與裝置相關聯的 GUID 格式字串。 |
| serialNumber     | 字串                  | 與裝置唯一相關聯的序號。 |
| productKey       | 字串                  | 與裝置唯一相關聯的產品金鑰。 |
| status           | 字串                  | 裝置資訊上傳的狀態：「進行中」、「已完成」、「已完成 \_ 但 \_ 發生錯誤」。 |
| errorCode        | 字串                  | 當裝置上傳失敗時傳回的 HTTP 狀態錯誤碼。 |
| errorDescription | 字串                  | 如果裝置上傳失敗，則為 HTTP 錯誤描述。 |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch**代表裝置的集合。

| 屬性     | 類型                                                           | 描述                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | 字串                                                         | 與裝置批次相關聯的 GUID 格式字串。 |
| createdBy    | 字串                                                         | 建立集合的租使用者名稱。                   |
| creationDate | UTC 日期時間格式的字串                                 | 建立集合的資料和時間。                    |
| deviceCount  | number                                                         | 集合中的裝置數目。                              |
| devicesLink  | [連結](utility-resources.md#link)                              | 包含在此批次中的裝置連結。                        |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest**提供建立裝置批次並在其中填入裝置所需的資訊。

| 屬性     | 類型                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | 字串                                                         | 與裝置批次相關聯的 GUID 格式字串。 |
| devices      | [裝置](#device)物件的陣列                             | 每個物件都會指定一個裝置。 已接受下列用於識別裝置的欄位組合： hardwareHash + productKey、hardwareHash + serialNumber、hardwareHash + productKey + serialNumber、hardwareHash only、僅 productKey、serialNumber + oemManufacturerName + modelName。 |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest**提供使用原則更新裝置清單所需的資訊。

| 屬性     | 類型                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | [裝置](#device)物件的陣列                             | 每個物件都會指定一個裝置。 需要下列屬性：識別碼、原則。 |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                              |
