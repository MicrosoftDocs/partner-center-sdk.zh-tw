---
title: 取得指定客戶的裝置批次清單
description: 如何為指定的客戶抓取裝置批次的集合。
ms.assetid: 46865031-E067-4FE3-9EC1-FE18F49F137A
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7dafb22639105321c0c13740f6404039e41ec5cd
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416603"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a>取得指定客戶的裝置批次清單


**適用於**

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何為指定的客戶抓取裝置批次的集合。

每個裝置批次都包含已註冊為零觸控部署之裝置的摘要狀態資訊。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取得指定客戶的裝置批次集合，請先使用客戶識別碼呼叫[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，以取得指定客戶上作業的介面。 然後，取出[**DeviceBatches**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches)屬性的值，以取得裝置批次集合作業的介面。 最後，呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync)方法來取出集合。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches = 
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： GetDevicesBatches.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1。1 |

 

**URI 參數**

建立要求時，請使用下列路徑參數。

| 名稱        | 類型   | 必要項 | 描述                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 客戶識別碼 | string | 是      | 識別客戶的 GUID 格式字串。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

無

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應

如果成功，回應主體會包含[DeviceBatch](device-deployment-resources.md#devicebatch)資源的集合。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 339
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "Test batch",
            "status": "finished",
            "creationDate": "2017-07-25T01:51:00",
            "devicesCount": 5,
            "devicesLink": {
                "uri": "/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/Test batch/devices",
                "method": "GET",
                "headers": []
            },
            "attributes": {
                "objectType": "DeviceBatch"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```