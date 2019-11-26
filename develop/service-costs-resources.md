---
title: Service costs resources
description: Describes resources related to services purchased by a customer.
ms.assetid: 2916B7F3-06D5-4DC1-A137-CD8270258CDB
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a7d08c740e0a338e1c8b09908b346257f60fe444
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488078"
---
# <a name="service-costs-resources"></a>Service costs resources

適用於：

- 合作夥伴中心

Describes resources related to services purchased by a customer.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** contains a summary that aggregates all services purchased by the specified customer during the billing period.

| 屬性 | 在工作列搜尋方塊中輸入 | 說明 |
| -------- | ---- | ----------- |
| details | array of [ServiceCostsSummaryDetail](#servicecostssummarydetail) objects | The service cost summary detail list, distinguished by invoice type.|
| links | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links. |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. |

> [!IMPORTANT]
> **The fields in the following table are being deprecated.** To retrieve recurring and one-time service cost summaries, use the **details** field instead. The **details** field is described in the previous table. Refer to the **details** field's corresponding data values but not the root-level fields.

| 屬性 | 在工作列搜尋方塊中輸入 | 說明 |
| -------- | ---- | ----------- |
| billingStartDate | date | The start of the billing period. |
| billingEndDate | date | The end of the billing period. |
| pretaxTotal | double | The pre-tax total of all costs for the customer. |
| tax  | double | The total tax incurred over all items purchased by the customer. |
| afterTaxTotal | double | The net total cost for all items purchased by the customer. |
| currencyCode | 字串 | Represents the currency used for the costs. |
| currencySymbol | 字串 | The currency symbol used for the costs. |
| customerId | 字串 | The ID of the customer making the purchase. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** describes a service cost summary that aggregates all services purchased by the specified customer during the billing period (from either recurring or one-time invoices).

| 屬性 | 在工作列搜尋方塊中輸入 | 說明 |
| -------- | ---- | ----------- |
| invoiceType | 字串 | The invoiceType that service cost summary has been generated. |
| summary | [ServiceCostsSummary](#servicecostssummary) | The service cost summary aggregated by a customer under one invoice type. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem** describes a single item purchased by the customer.

> [!IMPORTANT]
> The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**. These properties *don't apply to* service line items where the product is a *recurring purchase*. For example, these properties *don't apply* to subscription-based Office 365 and Azure.

| 屬性                 | 在工作列搜尋方塊中輸入                           | 說明                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | string in UTC date-time format | The start date for the charge.                                       |
| endDate                  | string in UTC date-time format | The end date for the charge.                                         |
| subscriptionFriendlyName | 字串                         | The friendly name for the subscription.                              |
| subscriptionId           | 字串                         | The subscription identifier.                                         |
| orderId                  | 字串                         | The order identifier.                                                |
| offerId                  | 字串                         | The offer identifier.                                                |
| offerName                | 字串                         | The offer name.                                                      |
| resellerMPNId            | 字串                         | Only used in 2-tier partner scenarios. Refers to the MPN identifier. |
| chargeType               | 字串                         | The associated charge type.                                          |
| quantity                 | 數目                         | The quantity of units used or purchased.                             |
| unitPrice                | 數目                         | The price per unit.                                                  |
| pretaxTotal              | 數目                         | The total charge for this item before taxes.                         |
| tax                      | 數目                         | The total tax charge incurred for this item.                         |
| afterTaxTotal            | 數目                         | The net total cost for this item.                                    |
| currencyCode             | 字串                         | Represents the currency used for the costs.                          |
| currencySymbol           | 字串                         | The currency symbol used for the costs.                              |
| customerId               | 字串                         | The ID of the customer making the purchase.                          |
| customerName             | 字串                         | The name of the customer making the purchase.                        |
| invoiceNumber            | 字串                         | The invoice number that this line item belongs to.                   |
| productId                | 字串                         | The product identifier.                                              |
| skuId                    | 字串                         | The Sku identifier.                                                  |
| availabilityId           | 字串                         | The availability identifier.                                         |
| productName              | 字串                         | The product name.                                                    |
| skuName                  | 字串                         | The sku name.                                                        |
| publisherName            | 字串                         | The publisher name.                                                  |
| publisherId              | 字串                         | The publisher identifier.                                            |
| termAndBillingCycle      | 字串                         | The term and billing cycle.                                          |
| discountDetails          | 字串                         | The discount details.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| 屬性             | 在工作列搜尋方塊中輸入                               | 說明                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [連結](utility-resources.md#link) | The URI to retrieve the line items. |
| self                 | [連結](utility-resources.md#link) | The self URI.                       |
