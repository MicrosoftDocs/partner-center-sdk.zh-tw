---
title: 客戶使用資源
description: 以使用量為基礎的訂用帳戶和每月使用預算（包括 CustomerMonthlyUsageRecord、Customerrelationshiprequest、PartnerUsageSummary 和 SpendingBudget）的客戶所適用的資源。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ec82fcfe6c08a8ad55dd1fb48984859b954dd3c8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094216"
---
# <a name="customer-usage-resources"></a>客戶使用資源

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

具有以使用量為基礎之訂用帳戶的客戶可能會有每月的使用預算。 此預算會針對客戶的最大使用量設定限制，並允許合作夥伴追蹤其使用時間。

> [!NOTE]
> 客戶使用量數位是估計值（不是最終的值），不應用於計費用途。

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord**代表客戶在當月使用的預估貨幣成本。

| 屬性         | 類型               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| 預算           | SpendingBudget     | 為客戶配置的消費預算。                          |
| PercentUsed      | decimal             | 已配置的預算所用的百分比。                        |
| ResourceId       | 字串             | 資源的唯一識別碼。                                   |
| ResourceName     | 字串             | 資源名稱。                                                |
| TotalCost        | decimal             | 訂用帳戶中資源使用量的預估總成本。|
| CurrencyLocale   | 字串             | 客戶的貨幣地區設定。 適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱。            |
| CurrencyCode     | 字串             | 取得或設定貨幣代碼。 適用于 Azure 方案。           |
| USDTotalCost     | decimal             | 取得或設定估計的總成本（美元）。 適用于 Azure 方案。                                         |
| IsUpgraded       | bool             | 取得或設定值，指出是否升級客戶的 Azure 訂用帳戶。 **True**值代表具有 Azure 方案的客戶。                         |
| LastModifiedDate | date               | 上次修改使用量資料的日期。                               |
| 屬性       | ResourceAttributes | 對應至使用記錄的中繼資料屬性。               |

## <a name="customerusagesummary"></a>Customerrelationshiprequest

**Customerrelationshiprequest**代表客戶在整個計費週期中的使用量摘要。

| 屬性         | 類型               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| 預算           | SpendingBudget     | 為客戶配置的消費預算。                                                                  |
| ResourceId       | 字串             | 資源的唯一識別碼。 在 CustomerMonthlyUsageRecord 的內容中，此識別碼是客戶識別碼。 |
| ResourceName     | 字串             | 資源名稱。 在 CustomerMonthlyUsageRecord 的內容中，這是客戶名稱。               |
| BillingStartDate | date               | 目前計費週期的開始日期。                                                                    |
| BillingEndDate   | date               | 目前計費週期的結束日期。                                                                      |
| TotalCost        | decimal             | 訂用帳戶中資源使用量的預估總成本。                                         |
| CurrencyLocale   | 字串             | 客戶的貨幣地區設定。 適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱。                                         |
| CurrencyCode     | 字串             | 取得或設定貨幣代碼。 適用于 Azure 方案。                                         |
| USDTotalCost     | decimal             | 取得或設定估計的總成本（美元）。 適用于 Azure 方案訂用帳戶資源。                                         |
| LastModifiedDate | date               | 上次修改使用量資料的日期。                                                                       |
| 連結            | ResourceLinks      | 對應至使用量摘要的資源連結。                                                           |
| 屬性       | ResourceAttributes | 對應至使用摘要的中繼資料屬性。                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary**代表所有客戶的使用量預算的夥伴層級摘要。

| 屬性         | 類型               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | 字串陣列   | 通知的電子郵件地址清單。                                                                   |
| CustomerOverBudget | integer          | 超過預算的客戶數目。                                                                    |
| CustomersTrendingOver | integer       | 接近預算的客戶數目。                                                     |
| CustomersWithUsageBasedSubscriptions  | integer | 具有以使用量為基礎之訂用帳戶的客戶數目。                                               |
| ResourceId       | 字串             | 資源的唯一識別碼。 在 CustomerMonthlyUsageRecord 的內容中，此識別碼是客戶識別碼。 |
| ResourceName     | 字串             | 資源名稱。 在 CustomerMonthlyUsageRecord 的內容中，這是客戶名稱。               |
| BillingStartDate | date               | 目前計費週期的開始日期。                                                                    |
| BillingEndDate   | date               | 目前計費週期的結束日期。                                                                      |
| TotalCost        | decimal             | 根據計費週期開始時的目前使用量，計算所有客戶使用量的預估總成本。      |
| CurrencyLocale   | 字串             | 貨幣地區設定。                                                                                             |
| LastModifiedDate | date               | 上次修改使用量資料的日期。                                                                       |
| 連結            | ResourceLinks      | 對應至使用量摘要的資源連結。                                                           |
| 屬性       | ResourceAttributes | 對應至使用摘要的中繼資料屬性。                                                      |

## <a name="spendingbudget"></a>SpendingBudget

**SpendingBudget**代表針對以使用量為基礎的訂用帳戶，配置給此客戶的預算。

| 屬性   | 類型               | Description                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| 數量     | decimal             | 已配置的預算。 如果值為 null，則不會配置給此客戶的消費預算。 |
| 屬性 | ResourceAttributes | 對應至預算的中繼資料屬性。                                                |
