---
title: Cart resources
description: A partner places an order when a customer wants to buy a subscription from a list of offers.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a9fb1c81cae0e7efa0a5e84d2b4d93e44ce7efb9
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489078"
---
# <a name="cart-resources"></a>Cart resources

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

A partner places an order when a customer wants to buy a subscription from a list of offers.

## <a name="cart"></a>Cart

Describes a cart.

| 屬性              | 在工作列搜尋方塊中輸入             | 說明                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | 字串           | A cart identifier that is supplied upon successful creation of the cart.                               |
| creationTimeStamp     | DateTime         | The date the cart was created, in date-time format. Applied upon successful creation of the cart.      |
| lastModifiedTimeStamp | DateTime         | The date the cart was last updated, in date-time format. Applied upon successful creation of the cart. |
| expirationTimeStamp   | DateTime         | The date the cart will expire, in date-time format. Applied upon successful creation of cart.          |
| lastModifiedUser      | 字串           | The user who last updated the cart. Applied upon successful creation of cart.                          |
| lineItems             | Array of objects | An Array of [CartLineItem](#cartlineitem) resources.                                                   |
| 狀態                | 字串           | The status of the cart. Possible values are "Active" (can be updated/submitted) and "Ordered" (has already been submitted). |

## <a name="cartlineitem"></a>CartLineItem

Represents one item contained in a cart.

| 屬性             | 在工作列搜尋方塊中輸入                             | 說明                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | 字串                           | A unique identifier for a cart line item. Applied upon successful creation of cart.                                                                   |
| catalogItemId        | 字串                           | The catalog item identifier.                                                                                                                          |
| friendlyName         | 字串                           | 選用。 The friendly name for the item defined by the partner to help disambiguate.                                                                 |
| quantity             | 整數                              | The number of licenses or instances.                                                                                                                  |
| currencyCode         | 字串                           | The currency code.                                                                                                                                    |
| billingCycle         | 物件                           | The type of billing cycle set for the current period.                                                                                                 |
| termDuration         | 字串                           | An ISO 8601 representation of the term's duration. The current supported values are P1M (1 month), P1Y (1 year) and P3Y (3 years).                                |
| 參與者         | List of Object String pairs      | A collection of PartnerId on Record (MPNID) on the purchase.                                                                                          |
| provisioningContext  | Dictionary<string, string>       | Additional context used when provisioning the purchased item. To determine which values are needed for a particular item please refer to the SKU's provisioningVariables property. |
| orderGroup           | 字串                           | A group to indicate which items can be submitted together in the same order.                                                                          |
| addonItems           | List of **CartLineItem** objects | A collection of cart line items for addons that will be purchased towards the base subscription that results from the root cart line item's purchase. |
| 錯誤 (error)                | 物件                           | Applied after cart is created in case of an error.                                                                                                    |
| renewsTo             | Array of objects                 | An array of [RenewsTo](#renewsto) resources.                                                                            |

## <a name="renewsto"></a>RenewsTo

Represents one item contained in a cart line item.

| 屬性              | 在工作列搜尋方塊中輸入             | 必要        | 說明 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | 字串           | 無              | An ISO 8601 representation of the renewal term's duration. The current supported values are **P1M** (1 month) and **P1Y** (1 year). |

## <a name="carterror"></a>CartError

Represents an error that occurs after a cart is created.

| 屬性         | 在工作列搜尋方塊中輸入                                   | 說明                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CartErrorCode](#carterrorcode) | The type of cart error.                                                                       |
| errorDescription | 字串                                 | The error description, including any notes about supported values, default values, or limits. |

## <a name="carterrorcode"></a>CartErrorCode

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate a type of cart error.

| 值                                | 位置 | 說明                                             |
|--------------------------------------|----------|---------------------------------------------------------|
| Unknown                              | 0        | 預設值。                                          |
| CurrencyIsNotSupported               | 10000    | The currency is not supported for the specified market. |
| CatalogItemIdIsNotValid              | 10001    | The catalog item ID is not valid.                       |
| QuotaNotAvailable                    | 10002    | There is not enough quota available.                    |
| InventoryNotAvailable                | 10003    | The inventory is not available for the selected offer.  |
| ParticipantsIsNotSupportedForPartner | 10004    | Setting participants is not supported for this partner. |
| UnableToProcessCartLineItem          | 10006    | Unable to process the cart line item.                   |
| SubscriptionIsNotValid               | 10007    | The subscription is not valid.                          |
| SubscriptionIsNotEnabledForRI        | 10008    | The subscription is not enabled for Azure reservations. |
| SandboxLimitExceeded                 | 10009    | The sandbox limit has been exceeded.                    |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Represents the result of a cart checkout.

| 屬性    | 在工作列搜尋方塊中輸入                                              | 說明                     |
|-------------|---------------------------------------------------|---------------------------------|
| orders      | List of [Order](order-resources.md#order) objects.         | The collection of orders.       |
| orderErrors | List of [OrderError](#ordererror) objects. | The collection of order errors. |

## <a name="ordererror"></a>OrderError

Represents an error that occurs during a cart checkout when an order is created.

| 屬性     | 在工作列搜尋方塊中輸入   | 說明                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | 字串 | The order group ID of the order with the error. |
| code         | 整數    | The error code.                                 |
| 描述  | 字串 | The description of the error.                   |

## <a name="ordererrorcode"></a>OrderErrorCode

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate a type of order error.

| 值 | 位置 | 說明 |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Partner Token missing in request context. |
| InvalidInput | 800002 | Invalid request input. |
| ServiceException | 800003 | Unexpected service error. |
| InvalidOfferId | 800004 | Invalid offer ID. |
| CreateOrderError | 800005 | Create order is not successful. |
| ProvisioningStatusNotFound | 800007 | Unable to retrieve provisioning information. |
| CartIdNotFound | 800008 | Unable to retrieve cart ID. |
| CartItemErrorInCreateOrder | 800009 | Error in Cart item(s). |
| InventoryNotAvailable | 800010 | Inventory is not available for this catalog item. |
| AzureSubscriptionNotValid | 800011 | This subscription is not a valid Azure subscription. |
| SubscriptionIsNotActive | 800012 | This subscription is not an active subscription. |
| SubscriptionIsNotEnabledForRI | 800013 | This subscription is not enabled for RI purchase. |
| PendingAdjustment | 800014 | There is a pending adjustment requested for this order. |
| MpnIdNotFound | 800015 | MPN Id is not found. |
| NotValidIndirectResellerMpnId | 800016 | MPN Id is not a valid Indirect Reseller. |
| InvalidQuantity | 800017 | The quantity is not available for this catalog item. |
| SandboxLimitExceeded | 800018 | The sandbox limit has been met. |
| SandboxTenantOnly | 800019 | This operation is only enabled for sandbox tenants. |
| CatalogItemNotEligibleForPurchase | 800020 | The catalog item is not eligible for purchase. |
| SubscriptionIsNotValid | 800021 | This subscription is not a valid subscription. |
| ManualReviewRequired | 800022 | You may be eligible for this transaction. Please contact Support for help.|
| InsufficientFunds | 800023 | You are not eligible for this transaction because your Credit Line is not reaching minimum threshold for this purchase.Please update your order(or) contact Support for help. |
| ReviewCancelled | 800024 | You are not eligible for this transaction. |
| LineOfCreditNotDefined | 800025 | You are not eligible for this transaction because your Credit Line is not reaching minimum threshold for this purchase. Please update your order (or) contact Support for help. |
| RiskError | 800026 | You are not eligible for this transaction. |
| SubscriptionNotRegistered | 800030 | This subscription is not registered. |
| PurchaseSystemNotSupported | 800031 | Purchase system not supported. |
| ConditionFailed | 800036 | Pre-condition failed. |
| AssetIdNotFound | 800037 | Asset ID not found. |
| AssetFutureBillingInfoNotFound | 800038 | Asset FutureBillingInfo not found. |
| ResellerProgramStatusNotActive | 800039 | Reseller program status is not active. |
| AssetStatusChangeNotValid | 800040 | Asset status cannot be changed to **{0}** from **{1}** . |
| ItemAlreadyActivated | 800041 | This item has already been activated. |
| NotSupported | 800042 | 未支援。 |
| PricingAccessForbidden | 800043 | Access to pricing information is not granted. |
| OrderInProgress | 800060 | Your order is in progress. Please check your order history for recent orders in few minutes. |
| OrderCannotBeCancelled | 800061 | Order cannot be cancelled. |
| ReviewRejected | 800062 | You are not eligible for this transaction. |
| CancelLegacyOrder | 800063 | This order **{0}** cannot be cancelled. Use `PATCH /customers/{1}/subscriptions/<subscriptionId>` to suspend subscriptions. |
| CartProcessedByAnotherRequest | 800064 | Cart **{0}** is being processed by another request. |
| CartCheckOutNotAllowedWhenStatusIsOrdered | 800065 | Cannot checkout an already submitted cart **{0}** . |
