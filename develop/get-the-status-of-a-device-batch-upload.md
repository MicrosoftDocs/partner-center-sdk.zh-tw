---
title: 取得裝置批次上傳的狀態
description: 如何為指定的客戶取得裝置批次上傳的狀態。
ms.assetid: 2965869E-824A-497E-9A77-6FC1BA18C55B
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0e60fad2247cf9e87f1b7e1b494e693c35d8fb8c
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416579"
---
# <a name="get-the-status-of-a-device-batch-upload"></a>取得裝置批次上傳的狀態


**適用於**

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心

如何為指定的客戶取得裝置批次上傳的狀態。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼。
- 提交裝置批次時，在位置標頭中傳回的批次追蹤識別碼。 如需詳細資訊，請參閱[上傳指定客戶的裝置清單](upload-a-list-of-devices-for-the-specified-customer.md)。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要取得裝置批次上傳的狀態，請先以客戶識別碼呼叫[**iaggregatepartner.customers.byid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)方法，以在指定的客戶上取得作業介面。 然後，使用 batch 追蹤識別碼呼叫[**BatchUploadStatus. ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid)方法，以取得批次上傳狀態作業的介面。 最後，呼叫[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get)或[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync)方法以取得狀態。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status = 
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**：合作夥伴中心 SDK 範例**類別**： GetBatchUploadStatus.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求語法**

| 方法  | 要求 URI                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1。1 |

 

**URI 參數**

建立要求時，請使用下列路徑參數。

| 名稱             | 類型   | 必要項 | 描述                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 客戶識別碼      | string | 是      | 識別客戶的 GUID 格式字串。                                                                                                                          |
| batchtracking-id | string | 是      | GUID 格式的識別碼，用來抓取裝置批次上傳狀態。 成功提交裝置批次時，此識別碼會在位置標頭中傳回。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

無

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應


如果成功，回應會包含[BatchUploadDetails](device-deployment-resources.md#batchuploaddetails)資源。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```