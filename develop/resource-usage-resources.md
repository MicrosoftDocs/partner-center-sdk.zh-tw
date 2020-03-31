---
title: 資源使用量記錄資源
description: 您可以使用 ResourceUsageRecord 資源來描述目前計費週期中訂用帳戶資源層級使用量的預估貨幣成本。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5a194a9ee2a7d9f4bffc2daf37a627e6b65a50e8
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415414"
---
# <a name="resource-usage-record-resources"></a>資源使用量記錄資源

適用於：

- 夥伴中心

您可以使用**ResourceUsageRecord**資源來描述目前計費週期中訂用帳戶資源層級使用量的預估貨幣成本。

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| 屬性         | 類型               | 描述                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | 取得或設定訂用帳戶識別碼。 若為 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶，此值為 commerce 訂閱識別碼。 若為 Azure 方案，此值為 Azure 方案識別碼）。                  |
| ResourceUri  | string             | 取得或設定資源 URI。」                                                        |
| ResourceType          | string             | 取得或設定資源類型。                                       |
| entitlementId               | string             | 取得或設定權利識別碼（Azure 訂用帳戶識別碼）。                                                 |
| EntitlementName             | string             | 取得或設定權利名稱。                                                     |
| resourceGroupName        | double             | 取得或設定資源組名。   |
| 名稱   | string             | 資源的名稱。 |
| ResourceName   | string             | 取得或設定資源的名稱。 |
| TotalCost   | decimal             | 取得或設定估計的總成本使用量。 |
| CurrencyCode   | string             | 取得或設定貨幣代碼。                                          |
| USDTotalCost   | decimal             | 取得或設定估計的總成本（美元）。                                         |
| lastModifiedDate | string             | 此記錄上次修改的日期（日期時間格式）。                             |
| 屬性       | ResourceAttributes | 對應至資源的中繼資料屬性。                                        |                                           |
