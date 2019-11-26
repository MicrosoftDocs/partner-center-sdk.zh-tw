---
title: Customer usage resources
description: Resources for customers with usage-based subscriptions and monthly use budgets (including CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary, and SpendingBudget).
ms.assetid: 268C7AF5-3A95-451F-8092-033A3E8126F2
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f94168e7f56e3e6c769c5a563e516046d7cc3509
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489818"
---
# <a name="customer-usage-resources"></a>Customer usage resources

適用於：

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Customers with usage-based subscriptions may have a monthly use budget. This budget sets a limit on the customer's maximum usage and allows the partner to track their usage over time.

> [!NOTE]
> Customer usage numbers are estimates (not final values), which should not be used for billing purposes.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** represents the estimated monetary cost of a customer's usage in the current month.

| 屬性         | 在工作列搜尋方塊中輸入               | 說明                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budget           | SpendingBudget     | The spending budget allocated for the customer.                          |
| PercentUsed      | 十進位             | The percentage used out of the allocated budget.                        |
| ResourceId       | 字串             | The unique identifier of the resource.                                   |
| ResourceName     | 字串             | The name of the resource.                                                |
| TotalCost        | 十進位             | The estimated total cost of usage for the resources in the subscription.|
| CurrencyLocale   | 字串             | The customer's currency locale. Available for Microsoft Azure (MS-AZR-0145P) subscriptions.            |
| CurrencyCode     | 字串             | Gets or sets the currency code. Available for Azure plans.           |
| USDTotalCost     | 十進位             | Gets or sets the estimated total cost in USD. Available for Azure plans.                                         |
| IsUpgraded       | bool             | Gets or sets a value indicating whether the customer's Azure subscription is upgraded. The value **true** represents customers who have an Azure plan.                         |
| LastModifiedDate | date               | The date the usage data was last modified.                               |
| 屬性       | ResourceAttributes | The metadata attributes corresponding to the usage record.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** represents a summary of the customer's usage for an entire billing period.

| 屬性         | 在工作列搜尋方塊中輸入               | 說明                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budget           | SpendingBudget     | The spending budget allocated for the customer.                                                                  |
| ResourceId       | 字串             | The unique identifier of the resource. In the context of CustomerMonthlyUsageRecord, this id is the customer id. |
| ResourceName     | 字串             | The name of the resource. In the context of CustomerMonthlyUsageRecord, this is the customer name.               |
| BillingStartDate | date               | The start date of the current billing period.                                                                    |
| BillingEndDate   | date               | The end date of the current billing period.                                                                      |
| TotalCost        | 十進位             | The estimated total cost of usage for the resources in the subscription.                                         |
| CurrencyLocale   | 字串             | The customer's currency locale. Available for Microsoft Azure (MS-AZR-0145P) subscriptions.                                         |
| CurrencyCode     | 字串             | Gets or sets the currency code. Available for Azure plans.                                         |
| USDTotalCost     | 十進位             | Gets or sets the estimated total cost in USD. Available for Azure plan subscription resources.                                         |
| LastModifiedDate | date               | The date the usage data was last modified.                                                                       |
| 連結            | ResourceLinks      | The resource links corresponding to the usage summary.                                                           |
| 屬性       | ResourceAttributes | The metadata attributes corresponding to the usage summary.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** represents a partner-level summary of usage budgeting for all customers.

| 屬性         | 在工作列搜尋方塊中輸入               | 說明                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | array of strings   | The list of email addresses for notifications.                                                                   |
| CustomerOverBudget | 整數          | The number of customers that are over budget.                                                                    |
| CustomersTrendingOver | 整數       | The number of customers that are close to going over budget.                                                     |
| CustomersWithUsageBasedSubscriptions  | 整數 | The number of customers with a usage-based subscription.                                               |
| ResourceId       | 字串             | The unique identifier of the resource. In the context of CustomerMonthlyUsageRecord, this id is the customer id. |
| ResourceName     | 字串             | The name of the resource. In the context of CustomerMonthlyUsageRecord, this is the customer name.               |
| BillingStartDate | date               | The start date of the current billing period.                                                                    |
| BillingEndDate   | date               | The end date of the current billing period.                                                                      |
| TotalCost        | 十進位             | The estimated total cost of all customer usage based on current usage from the start of the billing period.      |
| CurrencyLocale   | 字串             | The currency locale.                                                                                             |
| LastModifiedDate | date               | The date the usage data was last modified.                                                                       |
| 連結            | ResourceLinks      | The resource links corresponding to the usage summary.                                                           |
| 屬性       | ResourceAttributes | The metadata attributes corresponding to the usage summary.                                                      |

## <a name="spendingbudget"></a>SpendingBudget

**SpendingBudget** represents the budget allocated to this customer for usage-based subscriptions.

| 屬性   | 在工作列搜尋方塊中輸入               | 說明                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| 金額     | 十進位             | The allocated budget. If the value is null, there is no spending budget allocated to this customer. |
| 屬性 | ResourceAttributes | The metadata attributes corresponding to the budget.                                                |
