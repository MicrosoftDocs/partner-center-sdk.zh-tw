---
title: Meter usage record resource
description: You can use the MeterUsageRecord resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 003db39c92e96b12863edebb46b3e3341ffae10e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488308"
---
# <a name="meter-usage-record-resource"></a>Meter usage record resource

適用於：

- 合作夥伴中心

You can use the **MeterUsageRecord** resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.

## <a name="meterusagerecord"></a>MeterUsageRecord

| 屬性         | 在工作列搜尋方塊中輸入               | 說明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | 字串             | A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan. For Microsoft Azure (MS-AZR-0145P) subscriptions,, this value is the commerce subscription identifier. For Azure plan subscription resources, this value is the Azure plan identifier.                  |
| MeterId  | 字串             | Gets or sets the meter identifier.                                                        |
| MeterName          | 字串             | Gets or sets the meter name.                                       |
| 分類               | 字串             | Gets or sets the Azure resource category.                                                 |
| 子類別             | 字串             |  Gets or sets the Azure resource sub-category.                                                     |
| QuantityUsed        | 十進位             | Gets or sets the quantity of the Azure resource used.   |
| 單位   | 字串             | Gets or sets the unit of measure for the Azure resource. |
| TotalCost   | 十進位             | Gets or sets the estimated total cost of usage. |
| CurrencyLocale   | 字串             | The locale in which the subscription was used. This property determines the currency that is used on the invoice. This property is available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode   | 字串             | Gets or sets the currency code. This property is available for Azure plans.                                         |
| USDTotalCost   | 十進位             | Gets or sets the estimated total cost in USD. This property is available for Azure plans.                                         |
| LastModifiedDate | 字串             | The day (in date-time format) that this record was last modified.                             |
| 屬性       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |                                           |
