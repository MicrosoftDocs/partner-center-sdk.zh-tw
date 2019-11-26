---
title: Subscription usage resources
description: Subscription usage resources describe subscriptions with usage-based billing. These subscriptions have daily and monthly usage records, along with a usage summary for each pay period.
ms.assetid: 61B98AB8-D802-4EC1-91FB-B7A2B95DE20C
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 5b6c1a10023b22214bab89473b867a36c5a1eb7f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488018"
---
# <a name="subscription-usage-resources"></a>Subscription usage resources

適用於：

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

You can use the following subscription usage resources to get usage information for a specific subscription with usage-based billing. These subscriptions have daily and monthly usage records, along with a usage summary for each pay period.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*The **SubscriptionDailyUsageRecord** resource is obsolete and may produce inaccurate results. We recommend that you update your applications to use the APIs described in [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md) and [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) instead.*

The **SubscriptionDailyUsageRecord** resource describes how much a subscription is used in a single day.

| 屬性         | 在工作列搜尋方塊中輸入               | 說明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | 字串             | The day, in date-time format, that the subscription was used.                                 |
| ResourceId       | 字串             | GUID. The unique ID of the resource.                                                          |
| ResourceName     | 字串             | The name of the resource.                                                                     |
| TotalCost        | 十進位             | The estimated total cost of using the resources in the subscription on the specified day.     |
| CurrencyLocale   | 字串             | The locale in which the subscription was used, determines the currency to use on the invoice. |
| LastModifiedDate | 字串             | The day, in date-time format, that this record was last modified.                             |
| 屬性       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

The **SubscriptionMonthlyUsageRecord** resource describes how much a subscription is used in a single month.

| 屬性         | 在工作列搜尋方塊中輸入               | 說明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| 狀態           | 字串             | The status of the subscription: "none", "active", "suspended", or "deleted".                  |
| PartnerOnRecord  | 字串             | "The MPN ID of the partner on record."                                                        |
| OfferId          | 字串             | GUID. The id of the offer related to this subscription.                                       |
| Id               | 字串             | GUID. The id of the subscription or resource.                                                 |
| 名稱             | 字串             | The name of the subscription or resource.                                                     |
| TotalCost        | 十進位             | The estimated total cost of using the resources in the subscription in the specified month.   |
| CurrencyLocale   | 字串             | The locale in which the subscription was used, determines the currency to use on the invoice. Available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode     | 字串             | Gets or sets the currency code. Available for Azure plan subscription resources.                                         |
| USDTotalCost     | 十進位             | Gets or sets the estimated total cost in USD. Available for Azure plans.                                         |
| LastModifiedDate | 字串             | The day, in date-time format, that this record was last modified.                             |
| 屬性       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

The **SubscriptionUsageSummary** resource describes how much a specific subscription was used in the current billing period.

| 屬性         | 在工作列搜尋方塊中輸入               | 說明                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | 字串             | GUID. The id of the subscription or resource. In the context of CustomerMonthlyUsageRecord this id is the customer id. |
| ResourceName     | 字串             | The name of the subscription or resource. In the context of CustomerMonthlyUsageRecord this name is the customer name. |
| BillingStartDate | date               | The start date of the current billing period, in date-time format.                                                     |
| BillingEndDate   | date               | The end date of the current billing period, in date-time format.                                                       |
| TotalCost        | double             | The estimated total cost of using the resources in the subscription during the specified billing period.               |
| CurrencyLocale   | 字串             | The locale in which the subscription was used, determines the currency to use on the invoice. Available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode   | 字串             | Gets or sets the currency code. Available for Azure plans.                                         |
| USDTotalCost   | 十進位             | Gets or sets the estimated total cost in USD. Available for Azure plan subscription resources.                                         |
| LastModifiedDate | 字串             | The day, in date-time format, that this record was last modified.                                                      |
| 連結            | ResourceLinks      | The resource links corresponding to the SubscriptionUsageSummary.                                                      |
| 屬性       | ResourceAttributes | The metadata attributes corresponding to the SubscriptionUsageSummary.                                                 |
