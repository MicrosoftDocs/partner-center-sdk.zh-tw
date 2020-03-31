---
title: 取得發票語句
description: 使用發票識別碼抓取發票語句。
ms.assetid: 60EAA1F1-AFE2-4FC3-A475-4DBEA58583D1
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 4c93415e0722963dd881b03dcf9016be55edd212
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415882"
---
# <a name="get-invoice-statement"></a>取得發票語句

**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

使用發票識別碼抓取發票語句。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例僅支援使用「應用程式+使用者」認證來進行驗證。
- 有效的發票識別碼。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


若要依識別碼取得發票語句，請使用您的**ipartner.getinvoices**集合，並使用發票識別碼呼叫**ById （）** 方法，然後呼叫**Documents （）** 和**語句（）** 方法來存取 invoice 語句。 最後，呼叫**Get （）** 或**GetAsync （）** 方法。

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**範例**：[主控台測試應用程式](console-test-app.md)。 **專案**： PartnerSDK. FeatureSample**類別**： GetInvoiceStatement.cs 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求語法**

| 方法  | 要求 URI                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1。1  |


**URI 參數**

使用下列查詢參數來取得 invoice 語句。

| 名稱       | 類型       | 必要項 | 描述                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| 發票識別碼 | string     | 是      | 值是發票識別碼，可讓轉銷商篩選特定發票的結果。 |

 

**要求標頭**

- 如需詳細資訊，請參閱[標頭](headers.md)。

**要求本文**

無

**要求範例**

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 回應


如果成功，此方法會在回應主體中傳回[InvoiceStatement](invoice-resources.md#invoicestatement)資源。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

**回應範例**

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}  System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}  byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```