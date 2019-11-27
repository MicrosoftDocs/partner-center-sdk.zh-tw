---
title: 資源使用量記錄資源
description: 您可以使用 ResourceUsageRecord 資源來描述目前計費週期中訂用帳戶資源層級使用量的預估貨幣成本。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2ec59df657a5b49209da9e801dcfcae4a3282d56
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488088"
---
# <a name="resource-usage-record-resources"></a>資源使用量記錄資源

適用於：

- 合作夥伴中心

您可以使用**ResourceUsageRecord**資源來描述目前計費週期中訂用帳戶資源層級使用量的預估貨幣成本。

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| 屬性         | 類型               | 描述                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | 字串             | 取得或設定訂用帳戶識別碼。 若為 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶，此值為 commerce 訂閱識別碼。 若為 Azure 方案，此值為 Azure 方案識別碼）。                  |
| resourceUri  | 字串             | 取得或設定資源 URI。」                                                        |
| ResourceType          | 字串             | 取得或設定資源類型。                                       |
| entitlementId               | 字串             | 取得或設定權利識別碼（Azure 訂用帳戶識別碼）。                                                 |
| EntitlementName             | 字串             | 取得或設定權利名稱。                                                     |
| ResourceGroupName        | double             | 取得或設定資源組名。   |
| 名稱   | 字串             | 資源的名稱。 |
| ResourceName   | 字串             | 取得或設定資源的名稱。 |
| TotalCost   | 十進位             | 取得或設定估計的總成本使用量。 |
| CurrencyCode   | 字串             | 取得或設定貨幣代碼。                                          |
| USDTotalCost   | 十進位             | 取得或設定估計的總成本（美元）。                                         |
| lastModifiedDate | 字串             | 此記錄上次修改的日期（日期時間格式）。                             |
| 屬性       | ResourceAttributes | 對應至資源的中繼資料屬性。                                        |                                           |
