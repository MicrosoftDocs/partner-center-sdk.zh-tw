---
title: Offer resources
description: Describes a product listed in the reseller catalog that they can offer to their customers.
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 287482a934fecd73bce7d455098b3ab8a39d527c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486888"
---
# <a name="offer-resources"></a>Offer resources

**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Describes a product listed in the reseller catalog that they can offer to their customers.

## <a name="span-idofferspan-idofferspan-idofferoffer"></a><span id="Offer"/><span id="offer"/><span id="OFFER"/>Offer

| 屬性                    | 在工作列搜尋方塊中輸入                      | 說明                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | 字串                    | The offer identifier.                                                                                           |
| name                        | 字串                    | The offer name.                                                                                                 |
| 描述                 | 字串                    | A description of the offer.                                                                                     |
| minimumQuantity             | 整數                       | The minimum quantity available.                                                                                 |
| maximumQuantity             | 整數                       | The maximum quantity available.                                                                                 |
| rank                        | 整數                       | The offer rank or priority compared to other categories in the same product line. This property should be set only if there is more than one offer for a given product line.  |
| uri                         | 字串                    | The offer URI.                                                                                                  |
| locale                      | 字串                    | The locale in which the offer applies.                                                                          |
| 國家/地區                     | 字串                    | The country/region  where the offer applies.                                                                    |
| 類別                    | [OfferCategory](#offercategory)           | The category of the offer.                                                                   |
| limitUnitOfMeasure          | 字串                    | A value that indicates the type of purchase limitation. 可能的值包括：<br/> "None" - There are no restrictions on the number of subscriptions based on the offer purchased.<br/> "Concurrent" - The number of subscriptions that can exist on the customer tenant at a given time, this includes subscriptions that are active or canceled. This value applies mostly to small business offers where license counts are less than 300. De-provisionioned subscriptions don't count.<br/> "LifeTime" - The number of subscriptions that can exist for the lifetime of the customer tenant. This value is most applicable to Trials. De-provisionioned subscriptions don't count.      |
| limit                       | 整數                       | The amount of subscriptions that can be purchased of this offer based on the limitUnitOfMeasure.                |
| prerequisiteOffers          | 字串                    | The prerequisite offers.                                                                                        |
| isAddOn                     | boolean                   | A value indicating whether this instance is an addon.                                                           |
| hasAddOns                   | boolean                   | A value indicating whether this offer has any addons.                                                           |
| isAvailableForPurchase      | boolean                   | A value indicating whether this instance is available for purchase.                                             |
| 計費                     | 字串                    | Specifies the billing type for the line item purchase: "none", "usage", or "license".                           |
| supportedBillingCycles      | array of strings          | Indicates the billing cycles supported for this offer. Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | boolean                   | A value indicating whether the offer renews automatically.                                                      |
| upgradeTargetOffers         | array of strings          | The list of offers that this offer can be upgraded to.                                                          |
| conversionTargetOffers      | array of strings          | The list of offers that this offer can be converted to.                                                         |
| reselleeQualifications      | array of strings          | The qualifications required by the customer in order for a partner to purchase the offer for that customer.     |
| resellerQualifications      | array of strings          | The qualifications required by the partner in order to purchase the offer for a customer.                       |
| salesGroupId                | 字串                    | A string used to group offers into separate orders.                                                             |
| isTrial                     | boolean                   | A value indicating whether this is a trial offer.                                                               |
| product                     | [OfferProduct](#offerproduct)           | Gets the offer product.                                                                           |
| unitType                    | 字串                    | The type of the unit.                                                                                      |
| links                       | [OfferLinks](#offerlinks)               | The offer's "learn more" link.                                                                    |
| 屬性                  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the offer.                         |

## <a name="span-idoffercategoryspan-idoffercategoryspan-idoffercategoryoffercategory"></a><span id="OfferCategory"/><span id="offercategory"/><span id="OFFERCATEGORY"/>OfferCategory

Describes the categorization of an offer. This includes the rank or priority of this offer category compared to others in the same product line.

| 屬性   | 在工作列搜尋方塊中輸入                                                           | 說明                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | 字串                                                         | The category identifier.                                                                                                                                                   |
| name       | 字串                                                         | The category name.                                                                                                                                                         |
| rank       | 整數                                                            | The category rank or priority compared to other categories in the same offer. This property should be set only if there is more than one offer category for a given offer. |
| locale     | 字串                                                         | The locale in which the offer applies.                                                                                                                        |
| 國家/地區    | 字串                                                         | The country/region where the offer applies.                                                                                                                   |
| links      | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the OfferCategory.                                                                                                                     |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the OfferCategory.                                                                                                                |

## <a name="span-idofferlinksspan-idofferlinksspan-idofferlinksofferlinks"></a><span id="OfferLinks"/><span id="offerlinks"/><span id="OFFERLINKS"/>OfferLinks

Contains links for learning more information about the offer.

| 屬性  | 在工作列搜尋方塊中輸入 | 說明                 |
|-----------|------|-----------------------------|
| learnMore | Link | The "learn more" link.      |
| self      | Link | The self URI                |
| 下一步      | Link | The next page of items.     |
| previous  | Link | The previous page of items. |

## <a name="span-idofferproductspan-idofferproductspan-idofferproductofferproduct"></a><span id="OfferProduct"/><span id="offerproduct"/><span id="OFFERPRODUCT"/>OfferProduct

A product or service which may have more than one offer associated with it, each with different sets of features and targeted at different customer needs.

| 屬性 | 在工作列搜尋方塊中輸入   | 說明              |
|----------|--------|--------------------------|
| Id       | 字串 | The category identifier. |
| 名稱     | 字串 | The category name.       |
| 單位     | 字串 | The product unit.        |
