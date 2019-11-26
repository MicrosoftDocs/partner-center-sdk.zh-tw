---
title: Subscription resources
description: Subscription resources can provide further information about subscriptions throughout the life cycle, such as support, refunds, Azure entitlements.
ms.assetid: E99B5EC3-2247-4CAD-B651-3000E36AF6B6
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: dc771fcbc8cb03e95684dd32ff0f1f29076bba49
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486698"
---
# <a name="subscription-resources"></a>Subscription resources

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

A subscription lets a customer use a service for a certain period of time. Not all fields will apply to all subscriptions. Many fields only apply at certain points in the life cycle, such as if a subscription is suspended or cancelled.

## <a name="subscription"></a>訂閱

>[!NOTE]
>The **Subscription** resource has a rate limit of 500 requests per minute per tenant identifier.

The **Subscription** resource represents the life cycle of a subscription and includes properties that define the states throughout the subscription life cycle.

| 屬性             | 在工作列搜尋方塊中輸入                                                          | 說明                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | 字串                                                        | The subscription identifier.                                                                                                                                                  |
| offerId              | 字串                                                        | The offer identifier.                                                                                                                                                         |
| entitlementId        | 字串                                                        | The entitlement identifier (an Azure subscription ID).                                                                                                                        |
| offerName            | 字串                                                        | The offer name.                                                                                                                                                               |
| friendlyName         | 字串                                                        | The friendly name for the subscription defined by the partner to help disambiguate.                                                                                           |
| quantity             | 數目                                                        | The quantity. For example, in case of license-based billing, this property is set to the license count.                                                            |
| unitType             | 字串                                                        | The units defining quantity for the subscription.                                                                                                                             |
| parentSubscriptionId | 字串                                                        | Gets or sets the parent subscription identifier.                                                                                                                              |
| creationDate         | 字串                                                        | Gets or sets the creation date, in date-time format.                                                                                                                          |
| effectiveStartDate   | string in UTC date time format                                | Gets or sets the effective start date for this subscription, in date-time format. It is used to back date a migrated subscription or to align it with another.                |
| commitmentEndDate    | string in UTC date time format                                | The commitment end date for this subscription, in date-time format. For subscriptions which are not auto-renewable, this represents a date far, far away in the future.       |
| 狀態               | 字串                                                        | The subscription status: "none", "active", "pending", "suspended", or "deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Gets a value indicating whether the subscription is renewed automatically.                                                                                                    |
| billingType          | 字串                                                        | Specifies how the subscription is billed: "none", "usage", or "license".                                                                                                      |
| billingCycle         | 字串                                                        | Indicates the frequency with which the partner is billed for this order. Supported values are the member names found in [**BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Gets or sets a value indicating whether the subscription has purchasable add-ons.                                                                                             |
| isTrial              | boolean                                                       | A value indicating whether this is a trial subscription.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | A value indicating whether this is a Microsoft product.                                                                                                                       |
| publisherName        | 字串                                                        | The publisher name.                                                                                                                                                           |
| actions              | array of strings                                              | Gets or sets the actions that are allowed. Possible values: "edit", "cancel"                                                                                                  |
| partnerId            | 字串                                                        | The MPN ID of the reseller of record, used in the indirect partner model.                                                                                                     |
| suspensionReasons    | array of strings                                              | Read-only. If the subscription was suspended, indicates why.                                                                                                                  |
| contractType         | 字串                                                        | Read-only. The type of contract: "subscription", "productKey", or "redemptionCode".                                                                                           |
| refundOptions        | array of [RefundOption](#refundoption) resources   | Read-Only. The set of refund options available for this subscription.                                                                                              |
| links                | [SubscriptionLinks](#subscriptionlinks)                       | Gets or sets the subscription links.                                                                                                                                          |
| orderId              | 字串                                                        | The ID of the order that was placed to begin the subscription.                                                                                                                |
| termDuration         | 字串                                                        | An ISO 8601 representation of the term's duration. The current supported values are **P1M** (1 month), **P1Y** (1 year) and **P3Y** (3 years).                                                        |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the subscription.                                                                                                                    |
| renewalTermDuration  | 字串                                                        | An ISO 8601 representation of the term's duration. The current supported values are **P1M** (1 month) and **P1Y** (1 year).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

The **SubscriptionLinks** resource describes the collection of links attached to a subscription resource.

| 屬性           | 在工作列搜尋方塊中輸入                               | 說明                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [連結](utility-resources.md#link) | Gets or sets the offer.               |
| parentSubscription | [連結](utility-resources.md#link) | Gets or sets the parent subscription. |
| product            | [連結](utility-resources.md#link) | Gets the product associated with the subscription. |
| sku                | [連結](utility-resources.md#link) | Gets the product sku associated with the subscription. |
| 可用性       | [連結](utility-resources.md#link) | Gets the product sku availability associated with the subscription. |
| activationLinks    | [連結](utility-resources.md#link) | Gets the list of activation links associated with the subscription. |
| self               | [連結](utility-resources.md#link) | The self URI.                         |
| 下一步               | [連結](utility-resources.md#link) | The next page of items.               |
| previous           | [連結](utility-resources.md#link) | The previous page of items.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

The **SubscriptionProvisioningStatus** resource provides information about the provisioning status of a subscription.

| 屬性   | 在工作列搜尋方塊中輸入                                                           | 說明                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | 字串                                                         | A GUID formatted string that identifies the product SKU.             |
| 狀態     | 字串                                                         | Indicates the provisioning status: "success", "pending" or "failed". |
| quantity   | 數目                                                         | Provides the subscription quantity after provisioning.               |
| endDate    | string in UTC date time format                                 | The end date of the subscription.                                    |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

The **SubscriptionRegistrationStatus** resource describes the collection of links attached to a subscription resource.

| 屬性           | 在工作列搜尋方塊中輸入                               | 說明                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | 字串                             | The subscription identifier.                                                          |
| 狀態             | 字串                             | Indicates the registration status: "registered", "registering" or "notregistered".    |

## <a name="supportcontact"></a>SupportContact

The **SupportContact** resource represents a support contact for a customer's subscription.

| 屬性        | 在工作列搜尋方塊中輸入                                                           | 說明                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | 字串                                                         | A GUID formatted string that indicates the support contact's tenant identifier. |
| supportMpnId    | 字串                                                         | The contact's Microsoft Partner Network (MPN) identifier.                       |
| name            | 字串                                                         | The name of the support contact.                                                |
| links           | [ResourceLinks](utility-resources.md#resourcelinks)            | The support contact related links.                                              |
| 屬性      | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes. Contains "objectType": " SupportContact".              |

## <a name="registersubscription"></a>RegisterSubscription

The **RegisterSubscription** resource returns a link that can be used to query the registration status of a subscription. The registration status is returned in the response body of a successfully accepted request to register an Azure subscription.

| 屬性                | 在工作列搜尋方塊中輸入                               | 說明                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | 物件                             | Returns HTTP Status Code 202 "Accepted", with a Location header containing a link to query the registration status. 例如，`"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption

The **RefundOption** resource represents a possible refund option for the subscription.

| 屬性          | 在工作列搜尋方塊中輸入 | 說明                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| type | 字串 | The type of refund. The supported values are "Partial" and "Full" |
| expiresAfter      | string in UTC date time format | The timestamp when this option expires. If null, this means it has no expiration. |

## <a name="azureentitlement"></a>AzureEntitlement

The **AzureEntitlement** resource represents the Azure entitlements for the subscription.

| 屬性          | 在工作列搜尋方塊中輸入 | 說明                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | 字串 | The entitlement identifier |
| friendlyName      | 字串 | The friendly name of the entitlement. |
| 狀態 | 字串 | The status of entitlement. |
| subscriptionId | 字串 | The subscription identifier the entitlement belongs to. |
