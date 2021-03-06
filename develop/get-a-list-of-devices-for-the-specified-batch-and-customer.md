---
title: 取得指定批次和客戶的裝置清單
description: 如何在指定的裝置批次中，為客戶捕獲裝置和裝置詳細資料的集合。
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 125d1b4e239f69ae2dfc9667f5d009bab9f415b2
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927658"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>取得指定批次和客戶的裝置清單

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心

本文說明如何在指定的裝置批次中，為指定的客戶捕獲裝置集合。 每個裝置資源都包含裝置的詳細資料。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援對獨立應用程式和應用程式 + 使用者認證進行驗證。

- 客戶識別碼 (`customer-tenant-id`)。 如果您不知道客戶的識別碼，則可以在合作夥伴中心的[儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表中選取 [CSP]  ，然後選取 [客戶]  。 從 [客戶] 清單中選取客戶，然後選取 [帳戶]  。 在客戶的 [帳戶] 頁面上，尋找 [客戶帳戶資訊]  區段中的 [Microsoft 識別碼]  。 Microsoft 識別碼與客戶識別碼 (`customer-tenant-id`) 相同。

- 裝置批次識別碼。

## <a name="c"></a>C\#

若要在指定的裝置批次中，為指定的客戶取出裝置集合：

1. 使用客戶識別碼來呼叫 [**>iaggregatepartner.customers. >iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 方法，以取得指定之客戶的作業介面。

2. 呼叫 [**DeviceBatches. >iaggregatepartner.customers.byid**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) 方法，以針對指定的批次取得裝置批次集合作業的介面。

3. 取出 [**Devices**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) 屬性，以取得批次的裝置集合作業介面。

4. 呼叫 [**Get**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) 或 [**GetAsync**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync]) 方法，以取得裝置的集合。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

如需範例，請參閱下列內容：

- 範例： [主控台測試應用程式](console-test-app.md)
- 專案： **合作夥伴中心 SDK 範例**
- 類別： **GetDevices.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法  | 要求 URI                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1。1 |

#### <a name="uri-parameters"></a>URI 參數

建立要求時，請使用下列路徑參數。

| 名稱           | 類型   | 必要 | 描述                                           |
|----------------|--------|----------|-------------------------------------------------------|
| customer-id    | 字串 | Yes      | 用來識別客戶的 GUID 格式字串。 |
| devicebatch-id | 字串 | Yes      | 識別裝置批次的字串識別碼。 |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 回應

如果成功，回應主體會包含 [裝置](device-deployment-resources.md#device) 資源的分頁集合。 集合包含頁面中的100裝置。 若要取出100裝置的下一頁，回應主體中的 continuationToken 必須包含在後續要求中，以作為 ContinuationToken 標頭。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
