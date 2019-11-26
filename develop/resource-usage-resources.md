---
title: Resource usage record resources
description: You can use the ResourceUsageRecord resource to describe the estimated monetary cost of a subscription's resource level usage in the current billing cycle.
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
# <a name="resource-usage-record-resources"></a>Resource usage record resources

適用於：

- 合作夥伴中心

You can use the **ResourceUsageRecord** resource to describe the estimated monetary cost of a subscription's resource level usage in the current billing cycle.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| 屬性         | 在工作列搜尋方塊中輸入               | 說明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | 字串             | Gets or sets the subscription identifier. For Microsoft Azure (MS-AZR-0145P) subscriptions, this value is the commerce subscription identifier. For Azure plans, this value is the Azure plan identifier).                  |
| ResourceUri  | 字串             | Gets or sets the resource URI."                                                        |
| ResourceType          | 字串             | Gets or sets the resource type.                                       |
| EntitlementId               | 字串             | Gets or sets the entitlement identifier (the Azure subscription identifier).                                                 |
| EntitlementName             | 字串             | Gets or sets the entitlement name.                                                     |
| ResourceGroupName        | double             | Gets or sets the resource group name.   |
| 名稱   | 字串             | The name of the resource. |
| ResourceName   | 字串             | Gets or sets the name of the resource. |
| TotalCost   | 十進位             | Gets or sets the estimated total cost usage. |
| CurrencyCode   | 字串             | Gets or sets the currency code.                                          |
| USDTotalCost   | 十進位             | Gets or sets the estimated total cost in USD.                                         |
| LastModifiedDate | 字串             | The day (in date-time format) that this record was last modified.                             |
| 屬性       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |                                           |
