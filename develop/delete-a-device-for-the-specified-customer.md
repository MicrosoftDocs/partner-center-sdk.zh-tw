---
title: 為指定客戶刪除裝置
description: 如何刪除屬於指定之客戶的裝置。
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69b5440f2cf07d3cb4ecd5addf429acd64530257
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927823"
---
# <a name="delete-a-device-for-the-specified-customer"></a>為指定客戶刪除裝置

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

本文說明如何刪除屬於指定之客戶的裝置。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 裝置批次識別碼。

- 裝置識別碼。

## <a name="c"></a>C\#

若要為指定的客戶刪除裝置：

1. 使用客戶識別碼呼叫 [**>iaggregatepartner.customers >iaggregatepartner.customers.byid**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法，以抓取客戶的作業介面。

2. 使用裝置批次識別碼呼叫 [**DeviceBatches. >iaggregatepartner.customers.byid**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) 方法，以取得指定之批次的作業介面。

3. 呼叫 [**>iaggregatepartner.customers.byid**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) 方法，以取得要在指定裝置上操作的介面。

4. 呼叫 [**delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) 或 [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) 方法，從批次中刪除裝置。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

**範例**： [主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例 **類別**： DeleteDevice.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法     | 要求 URI                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| 刪除     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1。1  |

#### <a name="uri-parameters"></a>URI 參數

建立要求時，請使用下列路徑參數。

| 名稱           | 類型   | 必要 | 描述                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| customer-id    | 字串 | Yes      | 用來識別客戶的 GUID 格式字串。              |
| devicebatch-id | 字串 | Yes      | 包含裝置之批次的裝置批次識別碼。 |
| 裝置識別碼      | 字串 | Yes      | 裝置識別碼。                                             |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無

### <a name="request-example"></a>要求範例

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應會傳回 **204 沒有內容** 狀態碼。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
