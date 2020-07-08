---
title: 訂用帳戶使用資源
description: 訂用帳戶使用資源會以使用量為基礎的計費來描述訂閱。 這些訂用帳戶具有每日和每月使用量記錄，以及每個付款週期的使用量摘要。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8e23287d80f19084860f4597754448e81c01049f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095795"
---
# <a name="subscription-usage-resources"></a>訂用帳戶使用資源

**適用於：**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

您可以使用下列訂用帳戶使用量資源，以使用量為基礎的計費取得特定訂用帳戶的使用量資訊。 這些訂用帳戶具有每日和每月使用量記錄，以及每個付款週期的使用量摘要。

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

***SubscriptionDailyUsageRecord**資源已過時，可能會產生不正確的結果。建議您更新應用程式，以使用[取得 Azure 的客戶使用量記錄](get-a-customer-s-utilization-record-for-azure.md)中所述的 api，並改[為取得 Microsoft Azure 的價格](get-prices-for-microsoft-azure.md)。*

**SubscriptionDailyUsageRecord**資源描述一個訂用帳戶在一天內使用的數量。

| 屬性         | 類型               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | 字串             | 使用訂閱的日（以日期時間格式表示）。                                 |
| ResourceId       | 字串             | GUID。 資源的唯一識別碼。                                                          |
| ResourceName     | 字串             | 資源名稱。                                                                     |
| TotalCost        | decimal             | 在指定的日期，使用訂用帳戶中資源的預估總成本。     |
| CurrencyLocale   | 字串             | 使用訂閱的地區設定會決定要在發票上使用的貨幣。 |
| LastModifiedDate | 字串             | 上次修改此記錄的日期（以日期時間格式表示）。                             |
| 屬性       | ResourceAttributes | 對應至資源的中繼資料屬性。                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

**SubscriptionMonthlyUsageRecord**資源描述一個月內有多少訂用帳戶。

| 屬性         | 類型               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| 狀態           | 字串             | 訂用帳戶的狀態： [無]、[作用中]、[已暫停] 或 [已刪除]。                  |
| PartnerOnRecord  | 字串             | 「記錄上合作夥伴的 MPN 識別碼」。                                                        |
| OfferId          | 字串             | GUID。 與此訂用帳戶相關之供應專案的識別碼。                                       |
| Id               | 字串             | GUID。 訂用帳戶或資源的識別碼。                                                 |
| 名稱             | 字串             | 訂用帳戶或資源的名稱。                                                     |
| TotalCost        | decimal             | 在指定的月份中，使用訂用帳戶中資源的預估總成本。   |
| CurrencyLocale   | 字串             | 使用訂閱的地區設定會決定要在發票上使用的貨幣。 適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱。 |
| CurrencyCode     | 字串             | 取得或設定貨幣代碼。 適用于 Azure 方案訂用帳戶資源。                                         |
| USDTotalCost     | decimal             | 取得或設定估計的總成本（美元）。 適用于 Azure 方案。                                         |
| LastModifiedDate | 字串             | 上次修改此記錄的日期（以日期時間格式表示）。                             |
| 屬性       | ResourceAttributes | 對應至資源的中繼資料屬性。                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

**SubscriptionUsageSummary**資源描述在目前計費週期中使用的特定訂用帳戶數量。

| 屬性         | 類型               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | 字串             | GUID。 訂用帳戶或資源的識別碼。 在 CustomerMonthlyUsageRecord 的內容中，此識別碼是客戶識別碼。 |
| ResourceName     | 字串             | 訂用帳戶或資源的名稱。 在 CustomerMonthlyUsageRecord 的內容中，此名稱是客戶名稱。 |
| BillingStartDate | date               | 目前計費週期的開始日期（以日期時間格式）。                                                     |
| BillingEndDate   | date               | 目前計費週期的結束日期（以日期時間格式）。                                                       |
| TotalCost        | double             | 在指定的計費期間內，使用訂用帳戶中資源的預估總成本。               |
| CurrencyLocale   | 字串             | 使用訂閱的地區設定會決定要在發票上使用的貨幣。 適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱。 |
| CurrencyCode   | 字串             | 取得或設定貨幣代碼。 適用于 Azure 方案。                                         |
| USDTotalCost   | decimal             | 取得或設定估計的總成本（美元）。 適用于 Azure 方案訂用帳戶資源。                                         |
| LastModifiedDate | 字串             | 上次修改此記錄的日期（以日期時間格式表示）。                                                      |
| 連結            | ResourceLinks      | 對應至 SubscriptionUsageSummary 的資源連結。                                                      |
| 屬性       | ResourceAttributes | 對應至 SubscriptionUsageSummary 的中繼資料屬性。                                                 |
