---
title: 資源使用量記錄資源
description: 您可以使用 ResourceUsageRecord 資源來描述目前計費週期中訂用帳戶資源層級使用量的預估貨幣成本。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d58c3787a76c9dd1aa0e3d5cd90956f940d6de19
ms.sourcegitcommit: 42b4d44796df44c18460145acb5a63566d9153c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82089238"
---
# <a name="resource-usage-record-resources"></a>資源使用量記錄資源

**適用於：**

- 合作夥伴中心

您可以使用**ResourceUsageRecord**資源來描述目前計費週期中訂用帳戶資源層級使用量的預估貨幣成本。

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| 屬性         | 類型               | 描述                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | 字串             | 取得或設定訂用帳戶識別碼。 若為 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶，此值為 commerce 訂閱識別碼。 若為 Azure 方案，此值為 Azure 方案識別碼）。                  |
| ResourceUri  | 字串             | 取得或設定資源 URI。」                                                        |
| ResourceType          | 字串             | 取得或設定資源類型。                                       |
| EntitlementId               | 字串             | 取得或設定權利識別碼（Azure 訂用帳戶識別碼）。                                                 |
| EntitlementName             | 字串             | 取得或設定權利名稱。                                                     |
| resourceGroupName        | double             | 取得或設定資源組名。   |
| 名稱   | 字串             | 資源名稱。 |
| ResourceName   | 字串             | 取得或設定資源的名稱。 |
| TotalCost   | decimal             | 取得或設定估計的總成本使用量。 |
| CurrencyCode   | 字串             | 取得或設定貨幣代碼。                                          |
| USDTotalCost   | decimal             | 取得或設定估計的總成本（美元）。                                         |
| LastModifiedDate | 字串             | 此記錄上次修改的日期（日期時間格式）。                             |
| 屬性       | ResourceAttributes | 對應至資源的中繼資料屬性。                                        |                                           |
